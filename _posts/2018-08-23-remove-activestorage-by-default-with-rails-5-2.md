---
layout: post
title: Remove ActiveStorage by default with Rails 5.2
image: https://images.unsplash.com/photo-1489597148877-3c247b798b1e?ixlib=rb-0.3.5&ixid=eyJhcHBfaWQiOjEyMDd9&s=615335343eeacb5a1937ce63d3787e2f&auto=format&fit=crop&w=1452&q=80
---

When you make a new Rails 5 project and take a look at the default routes that come out-of-the-box, you will see something like this:

```
                  Prefix Verb URI Pattern                                                                              Controller#Action
       rails_service_blob GET  /rails/active_storage/blobs/:signed_id/*filename(.:format)                               active_storage/blobs#show
rails_blob_representation GET  /rails/active_storage/representations/:signed_blob_id/:variation_key/*filename(.:format) active_storage/representations#show
       rails_disk_service GET  /rails/active_storage/disk/:encoded_key/*filename(.:format)                              active_storage/disk#show
update_rails_disk_service PUT  /rails/active_storage/disk/:encoded_token(.:format)                                      active_storage/disk#update
     rails_direct_uploads POST /rails/active_storage/direct_uploads(.:format)                                           active_storage/direct_uploads#create
```

This is because Rails 5.2 sets as default the usage of ActiveStorage.

I do not know if this is what most projects need, but I do know that this is extra baggage that many of my applications do not need.

If you have already started your project and you would like to get rid of this, [here](https://mikerogers.io/2018/04/13/remove-activestorage-from-rails-5-2.html) is a good guide that will walk you through the process of removing ActiveStorage.

But if you are just about to start a new project, and you would like the site generator to give a fresh application without this feature activated by default, you can use the following command.

```bash
rails new my_project_name --skip-active-storage
```

This way you will find a clean new site without any use of ActiveStorage.
