## Git Backend Development Wiki / Guide / Stream of Conscience

### Gem Options
There are a number of gems that could be used. Here is a short outline of each. At one point the git gem was depreciated but now it appears that both are under active development. Reading through the Documentation of both it appears they support a majority of common git commands.

[**rugged**](https://rubygems.org/gems/rugged)

[**git**](http://rubygems.org/gems/git)

rugged is more efficient and more actively maintained. I'm sticking with the gem previously chosen.

## Installing Ruby/Gems
If you installed your environment according to one of the guides on the Wiki, chances are you will be required to update your environment to support rugged. 

The following are the steps taken with Ubuntu 12.04 LTS running in a Virtual Box.

###Set up rvm

`$ sudo apt-get install build-essential git-core`

`$ sudo apt-get install curl`

`$ \curl -sSL https://get.rvm.io | bash -s stable`

Now, you may need to configure your shell to use rvm. 
Enter 

`$ type rvm | head -1`

and if `rvm is a function` is not the output, go to Terminal Edit>Profile Preferences>Title and Command and ensure "Run command as a login shell" is selected. Try that line again and continue.

`$ rvm install 1.9.3`

Confirm that it is the current version being used. 

`$ rvm list`

If 1.9.3 is not the selected ruby version `$ rvm use 1.9.3` should switch it accordingly.

Onto the bundle install. This can be a rough go - known issues are the pg gem. If another one fails, it most likely is due to a connection issue. Try installing it on its own to diagnose the issue.

`$ sudo apt-get install libpq-dev` # required for pg gem

`$ gem install nodejs` # some ubuntu reason here (noted by Sheng and Zach)

`$ bundle install --without sqlite mysql` # assumes PostgreSQL. YMMV for other ones.

That's for the base MarkUs install. 

Fun notes: `$ require 'fastercsv'` and `$ require 'rubygems'` will throw an error and return false, respectively. Since the update (past 1.8) they are called 'csv' and baked directly into ruby, respectively. `$ require 'ruby-debug'` should still return true, however.

###Git specific gem installation 

Copied from [this previous MarkUs dev blog post](http://blog.markusproject.org/?p=5262)

Best to install libgit2 somewhere else from MarkUs less you want to deal with ignoring the files on every subsequent git commit.

`$ sudo apt-get install cmake`

`$ git clone https://github.com/libgit2/libgit2.git`

`$ cd libgit2`

`$ mkdir build`

`$ cd build`

`$ cmake ..`

`$ cmake --build .`

`$ gem install rugged`
