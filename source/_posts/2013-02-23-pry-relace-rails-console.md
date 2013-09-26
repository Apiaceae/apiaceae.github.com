--- 
layout: post 
title: 使用PRY代替RAILS CONSOLE 
date: 2013-09-23 15:30
sharing: true
comments: true
categories: Ruby
tags: [pry, debug]
---

rails默认的调度工具是ruby-debug19，启动时还要加上”–debug”参数，或许你觉得用起来也还可以。但如果你用过pry，你会发现原来可以还这么方便，ruby-debug19是那么的简陋。以前还整过一堆插件来增强irb的功能，现在有了pry，默认配置就够用了，还有rails console也可以歇歇了。

## 安装

**在Gemfile中添加**

``` ruby
gem 'pry', :group => :development
```

**然后执行**
``` ruby
bundle install
```
即可。

**它可以这样用**

**用pry代替irb方法，直接运行**：
``
pry
``

**用pry代替rails console方法，运行：**
``
pry -r ./config/environment.rb
``

**调试rails方法：**

直接在要调试的地方添加
``binding.pry``

``rails server``当运行到这行代码时会自动调出一个pry终端，可以在这里进行交互。退出调试用''exit-all''。

如：``/app/controllers/articles_controller.rb``

``` ruby
def index
  @articles = Article.all
  binding.pry
end
```

## 常用命令

**cd**: 这可不是切换目录的，而是切换类。如``cd Article``会进入Article类中，``Article.all``可直接缩写为``all``

**nesting: ** cd切来切去如果迷了路，用它可以看当前在哪个类下面。我倒觉得如果名字改为”pwd”会更好。

**ls**: 查看一些信息，ls -h查看帮助，ls -m查看实例方法，ls-M查看类方法，ls -p查看private方法。

**show-doc Array\#in\_groups\_of**：查看文档。

**show-method -l Array\#in\_groups\_of**：查看方法的源代码，-l显示行号。

**edit-method Array\#in\_groups\_of**：调出nano来编辑代码，如果是能调出vim就好啦。(后来发现其实很简单，见后面。)

**help**：显示帮助

## 调试Rails

pry默认没有调试中经常用到的下一步，上一步等命令，要安装
``
gem "pry-nav"
``
**然后就可以使用step, next, continue来跳来跳去了。**

## edit和edit-method能自动调用vim


默认调出nano编辑源代码是因为系统环境变量中没有\$EDITOR的缘故，有两种方法改为vim。
1、添加环境变量\$EDITOR=”vim”
2、新建\~/.pryrc配置文件，添加
``Pry.config.editor = "vim"
``

更多参考：

http://railscasts.com/episodes/280-pry-with-rails?view=asciicast

https://github.com/pry/pry

http://tyok.org/prying\_ruby/

http://blog.tyraeltong.com/blog/2011/10/14/introducing-pry

http://gnepud.tumblr.com

http://rubyer.me/blog/1585/

**下面是Pry—Hirb-awsom-print三个Gem包配合使用的.pryrc配置文件**

``` ruby
Pry.config.editor = "mvim"

####` Launch Pry with access to the entire Rails stack.
####' If you have Pry in your Gemfile, you can pass: ./script/console --irb=pry instead.

####` If you don't, you can load it through the lines below :)

rails = File.join Dir.getwd, 'config', 'environment.rb'
if File.exist?(rails) && ENV['SKIP\_RAILS'].nil?

require rails 

if Rails.version[0..0] == "2"

require 'console\_app'

require 'console\_with\_helpers'

elsif Rails.version[0..0] == "3"

require 'rails/console/app'

require 'rails/console/helpers'

\# Show sql output

ActiveRecord::Base.logger = Logger.new(STDOUT) if defined?
ActiveRecord::Base

\# Add reload! command if rails version \> 3.2

if Rails.version[2..2].to\_i \>= 2

include Rails::ConsoleMethods

end

else

warn "[WARN] cannot load Rails console commands (Not on Rails2 or
Rails3?)"

end

end

\# To edit the method given by editor mvim

class Object

def mvim(method\_name)

file, line = method(method\_name).source\_location

\`mvim '\#{file}' +\#{line}\`

end

end
 

\# Break out of the Bundler jail

\# from
https://github.com/ConradIrwin/pry-debundle/blob/master/lib/pry-debundle.rb

if defined? Bundler

Gem.post\_reset\_hooks.reject! { |hook| hook.source\_location.first =\~
%r{/bundler/} }

Gem::Specification.reset

load 'rubygems/custom\_require.rb'

end

 

if defined? Rails

begin

require 'hirb'

rescue LoadError

end

 

if defined? Hirb

\# Dirty hack to support in-session Hirb.disable/enable

Hirb::View.instance\_eval do

def enable\_output\_method

@output\_method = true

Pry.config.print = proc do |output, value|

Hirb::View.view\_or\_page\_output(value) ||
Pry::DEFAULT\_PRINT.call(output, value)

end

end

 

def disable\_output\_method

Pry.config.print = proc { |output, value|
Pry::DEFAULT\_PRINT.call(output, value) }

@output\_method = nil

end

end

 

Hirb.enable

end

end

 

begin

require 'awesome\_print'

rescue LoadError

end
```
