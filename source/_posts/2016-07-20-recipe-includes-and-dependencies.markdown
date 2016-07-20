---
layout: post
title: "Recipe Includes and Dependencies"
date: 2016-07-20 09:03:23 +0000
comments: true
categories: Chef
---

Create a new cookbook

```
knife cookbook create php
```

Change the Recipes

```ruby php/recipes/default.rb

package "php" do
  action :install
end

```

Change the apache cookbook's metadata

```ruby apache/metadata.rb

### Added this
depends "php"

```

```ruby apache/recipes/default.rb

include_recipe "php::default"

```

So that all. Easy
