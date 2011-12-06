!SLIDE
# Ruby Web Apps with Sinatra
## North Florida Ruby Brigade
6 December 2011

!SLIDE bullets incremental transition=fade
# Who is Sinatra?

* An amazing singer and performer
* Member of the 'Rat Pack'
* Kickass, minimalist web framework

!SLIDE transition=fade
# Hello World

!SLIDE transition=fade

    @@@shell
    $ gem install sinatra

!SLIDE transition=fade

    @@@ruby
    # sinatra_demo/app.rb
    require 'sinatra
    
    get '/' do
      'Hello World!'
    end
    
!SLIDE transition=fade

    @@@shell
    $ ruby -rubygems app.rb  # http://localhost:4567

!SLIDE transition=fade
# Extending Hello World
## Templates

!SLIDE transition=fade

    @@@html
    <!-- sinatra_demo/views/index.erb -->
    <html>
      <head>
        <title>Sinatra Demo</title>
      </head>
      <body>
        <h1>Hello World!</h1>
        <p>The time is <%= @current_time %>.</p>
      </body>
    </html>
    
!SLIDE transition=fade

    @@@ruby
    # sinatra_demo/app.rb
    require 'sinatra'
    
    class App < Sinatra::Application
      get '/' do
        @current_time = Time.now
      
        # Render views/index
        erb :index
      end
    end
    
!SLIDE transition=fade
  
    @@@html
    <!-- sinatra_demo/views/layout.html.erb -->
    <html>
      <head>
        <title>Sinatra Demo</title>
      </head>
      <body>
        <%= yield %>
      </body>
    </html>
    
    <!-- sinatra_demo/views/index.erb -->
    <h1>Hello World!</h1>
    <p>The time is <%= @current_time %>.</p>
    
!SLIDE transition=fade

    @@@ruby
    require 'sinatra'
    
    class App < Sinatra::Application
      get '/' do
        @current_time = Time.now
      
        # Render views/index
        # Automatically pulls in layout.html.erb
        erb :index
      end
    end
    
!SLIDE transition=fade
# Development

!SLIDE transition=fade

    $ gem install shotgun
    $ shotgun app.rb
    
!SLIDE bullets incremental transition=fade
# Development

* Shotgun uses Unix model of forking for requests
* Does not work on Windows or JRuby

!SLIDE transition=fade
# Deployment

!SLIDE transition=fade

    @@@ruby
    # config.ru
    require './app'
    
    run App
    

    