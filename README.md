# About Jekyll
https://jekyllrb.com/
# Install Jekyll

Run this command:
```
A new release of RubyGems is available: 3.5.18 → 3.5.22!
Run `gem update --system 3.5.22` to update your installation.

❯ sudo gem install bundler jekyll
Successfully installed bundler-2.5.22
Parsing documentation for bundler-2.5.22
Done installing documentation for bundler after 0 seconds
Successfully installed jekyll-4.3.4
Parsing documentation for jekyll-4.3.4
Done installing documentation for jekyll after 0 seconds
2 gems installed
```


# Install Ruby

```json
❯ ruby -v
ruby 2.6.10p210 (2022-04-12 revision 67958) [universal.arm64e-darwin23]
❯ echo 'export PATH="/opt/homebrew/opt/ruby/bin:$PATH"' >> ~/.zshrc
❯ export LDFLAGS="-L/opt/homebrew/opt/ruby/lib"
❯ export CPPFLAGS="-I/opt/homebrew/opt/ruby/include"
❯ ruby -v
ruby 3.3.5 (2024-09-03 revision ef084cc8f4) [arm64-darwin23]
```

# Start app local
Run this command
```
sudo bundle install
```
run this command:
```
bundle exec jekyll serve
```

Access to local page: Server address: http://127.0.0.1:4000/