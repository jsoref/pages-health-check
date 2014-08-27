# GitHub Pages Health Check

*Checks your GitHub Pages site for commons DNS configuration issues*

## Installation

`gem install github-pages-health-check`

## Usage

### Basic Usage

```ruby
> check = GitHubPages::HealthCheck.new("choosealicense.com")
=> #<GitHubPages::HealthCheck @domain="choosealicense.com" valid?=true>
> check.valid?
=> true
```

### An invalid domain

```ruby
> check = GitHubPages::HealthCheck.new("foo.github.com")
> check.valid?
=> false
> check.valid!
=> GitHubPages::HealthCheck::InvalidCNAME
```


### Retrieving specific checks

``` ruby
> check.should_be_a_record?
=> true
> check.a_record?
=> true
```

### Getting checks in bulk

```
> check.to_hash
=> {
 :cloudflare_ip?=>false,
 :old_ip_address?=>false,
 :a_record?=>true,
 :cname_record?=>false,
 :valid_domain?=>true,
 :apex_domain?=>true,
 :should_be_a_record?=>true,
 :pointed_to_github_user_domain?=>false,
 :pages_domain?=>false,
 :valid?=>true
}
> require 'json'
> check.to_json
=> "{\"cloudflare_ip?\":false,\"old_ip_address?\":false,\"a_record?\":true,\"cname_record?\":false,\"valid_domain?\":true,\"apex_domain?\":true,\"should_be_a_record?\":true,\"pointed_to_github_user_domain?\":false,\"pages_domain?\":false,\"valid?\":true}"
```