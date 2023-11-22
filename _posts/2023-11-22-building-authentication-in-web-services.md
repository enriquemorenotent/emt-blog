---
layout: post
title: "Building Authentication in Web Services"
categories: "web development"
image: images/jwt.png
excerpt: "How to build authentication in web services using JSON Web Tokens (JWTs) using Express in the backend and React in the frontend."
---

## Introduction
Hey there, future web service builders! Planning to create a separate FE and BE for your next awesome project? That's a great move! And let's not forget, every top-notch service needs robust authentication. So, let's dive into the world of JWT tokens, ensuring you're up there with the cool kids!

## Understanding JWT Tokens
When you log in to your web service, you typically receive an access token. This token proves your identity and is short-lived for security purposes. To avoid frequent logins, there's also a refresh token, which helps generate a new access token once the old one expires.

## Initial Approach
Here's how I initially thought to manage this:

1. Create both tokens during login.
2. Send them back in the response body.
3. Store them in the client's local storage.
4. Attach the access token to the header for every request.
5. On receiving a 401 error (indicating token expiration), request a new token via an endpoint like /auth/refresh.
6. Use the new access token to retry the failed request.

### Backend Login Request Handling

```javascript
// Backend: Handling /login request
app.post('/login', (req, res) => {
  const user = { /* user details */ };
  const accessToken = generateAccessToken(user);
  const refreshToken = generateRefreshToken(user);
  res.json({ accessToken, refreshToken });
});

function generateAccessToken(user) {
  return jwt.sign(user, process.env.ACCESS_TOKEN_SECRET, { expiresIn: '15m' });
}

function generateRefreshToken(user) {
  return jwt.sign(user, process.env.REFRESH_TOKEN_SECRET);
}

// Refreshing the access token
app.post('/auth/refresh', (req, res) => {
  const refreshToken = req.body.refreshToken;
  jwt.verify(refreshToken, process.env.REFRESH_TOKEN_SECRET, (err, user) => {
	if (err) return res.sendStatus(403);
	const accessToken = generateAccessToken({ name: user.name });
	res.json({ accessToken });
  });
});

```
### Backend Middleware for Access Token Verification
```javascript
// Middleware for token verification
function authenticateToken(req, res, next) {
  const token = req.headers['authorization']?.split(' ')[1];
  if (token == null) return res.sendStatus(401);

  jwt.verify(token, process.env.ACCESS_TOKEN_SECRET, (err, user) => {
    if (err) return res.sendStatus(401);
    req.user = user;
    next();
  });
}
```

### React Custom Hook with Axios

```javascript
// React: Custom hook for API calls with Axios
import axios from 'axios';

export const useAxios = () => {
  const axiosInstance = axios.create({
    baseURL: 'http://your-api.com',
  });

  axiosInstance.interceptors.response.use(response => response, async error => {
    const originalRequest = error.config;
    if (error.response.status === 401 && !originalRequest._retry) {
      originalRequest._retry = true;
      const { data } = await axios.post('/auth/refresh', { refreshToken: localStorage.getItem('refreshToken') });
      localStorage.setItem('accessToken', data.accessToken);
      originalRequest.headers['Authorization'] = 'Bearer ' + data.accessToken;
      return axiosInstance(originalRequest);
    }
    return Promise.reject(error);
  });

  return axiosInstance;
};
```

## Reevaluating the Approach
It turns out, my initial plan wasn't the best. Storing tokens in local storage posed security risks, and the entire process was inefficient, with multiple edge cases like race conditions. Plus, managing tokens in FE frameworks like React can get really complex.

## A Better Way - HttpOnly Cookies
Switching to HttpOnly cookies enhances security and streamlines token management.
Unlike tokens stored in local storage, HttpOnly cookies are **NOT** accessible via JavaScript, significantly reducing the risk of XSS attacks. The server handles token renewal and expiry transparently, providing a smoother user experience and reducing client-side complexity.

### Backend Setup with Access and Refresh Tokens

```javascript
// Backend: Generating both Access and Refresh Tokens
app.post('/login', (req, res) => {
  const user = { /* user details */ };
  const accessToken = generateAccessToken(user);
  const refreshToken = generateRefreshToken(user);
  res.cookie('accessToken', accessToken, { httpOnly: true, secure: true });
  res.cookie('refreshToken', refreshToken, { httpOnly: true, secure: true });
  res.json({ message: 'Logged in successfully' });
});
```

### Backend Middleware for Access Token Verification
```javascript
function verifyAndRenewToken(req, res, next) {
  const accessToken = req.cookies['accessToken'];
  const refreshToken = req.cookies['refreshToken'];

  jwt.verify(accessToken, process.env.ACCESS_TOKEN_SECRET, (err, userData) => {
    if (err && err.name === 'TokenExpiredError') {
      // Renew access token if expired
      jwt.verify(refreshToken, process.env.REFRESH_TOKEN_SECRET, (refreshErr, refreshUserData) => {
        if (refreshErr) {
          return res.sendStatus(403); // Invalid refresh token
        }
        const newAccessToken = generateAccessToken(refreshUserData);
        res.cookie('accessToken', newAccessToken, { httpOnly: true, secure: true });
        req.user = refreshUserData;
        next();
      });
    } else if (err) {
      // Other errors with access token
      return res.sendStatus(403);
    } else {
      // Access token is valid
      req.user = userData;
      next();
    }
  });
}

// Route using the external middleware
app.get('/some-protected-route', verifyAndRenewToken, (req, res) => {
  // Example content returned from the protected route
  res.json({ message: 'Access to protected content successful', content: 'Foo' });
});

```

## Conclusion
With these enhancements, your web service now securely manages JWT tokens using HttpOnly cookies. The backend handles both access and refresh tokens, ensuring seamless user experience, while the frontend's Axios setup respects cross-origin security. This setup not only boosts security but also simplifies token management in your FE/BE architecture.

