
## Jekyll Installation
Swap out `rbenv` below for `rvm` if you prefer. RVM was giving me installation issues, so I found `rbenv` - Travis

1. Create and run from a fresh VM instance:
    1. `gcloud compute instances create jekyll --image-project=ubuntu-os-cloud --image-family=ubuntu-1404-lts --machine-type=n1-standard-1`
    1. `gcloud compute ssh jekyll --ssh-flag="-L 4000:localhost:4000"`
1. Install `rbenv` and `ruby-build`. Add these to `$PATH`:
    1. `sudo apt-get install -y git bzip2 build-essential libssl-dev libreadline-dev zlib1g-dev`
    1. `git clone https://github.com/rbenv/rbenv.git ~/.rbenv`
    1. `git clone https://github.com/rbenv/ruby-build.git ~/.rbenv/plugins/ruby-build`
    1. `echo 'export PATH="$HOME/.rbenv/bin:$PATH"' >> ~/.bashrc`
    1. `echo 'eval "$(rbenv init -)"' >> ~/.bashrc`
    1. `. ~/.bashrc`
1. Install and use ruby 2.4.1    
    1. `rbenv install 2.4.1`
    1. `rbenv global 2.4.1`
1. Fork and clone your forked repo:
    1. `GITHUB_USER=$USER # or something else here`
    1. `git clone https://github.com/$GITHUB_USER/spinnaker.github.io.git`
1. Install `bundle` gem
    1. `cd spinnaker.github.io`
    1. `gem install bundle`
    1. `bundle install`    

## Local Development 
1. Start Jekyll server
    1. `bundle exec jekyll serve --watch`
1. (Optional): Add `--incremental` to speed up page generation when working on one page
    1. `bundle exec jekyll serve --watch --incremental`
1. Navigate to [http://localhost:4000](http://localhost:4000) to see your locally generated page.    


### Page Generation

A page named `foo.md` will be transformed to `foo/index.html` and links to `foo` will result in an HTTP 301 
to `foo/`. This has two implications:

1. It is more efficient to include the trailing `/` in links.
2. If you anticipate including resources like images or subpages, create `foo/index.md` instead of `foo.md`.

> During local development, see what's actually generated by browsing the `_site` directory.

## Mermaid

Sequence diagrams can be generated with the [mermaid.js](https://github.com/knsv/mermaid) library by adding `{% 
include mermaid %}` near the bottom of the page. See some of the 
[security docs](https://github.com/spinnaker/spinnaker.github.io/blob/master/setup/security/authentication/index.md)
for an example.

## Breadcrumbs

Each page has a breadcrumb trail at the top that is based on the URL structure. You should ensure that there is at 
least an `index.md` file within each URL directory, otherwise the links will break.

## Link Checker

Run link checker before committing: 
`rake test`

(TODO: enforce this via CI build?)