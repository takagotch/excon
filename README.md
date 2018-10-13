### excon
---

https://github.com/excon/excon

```
sudo gem install excon


```

```ruby
require 'rubygem'
require 'excon'

response = Excon.get('http://geemus.com')
response.body # => "..."
response.headers # => {...}
response.remote_ip # => "..."
response.status # => 200

connection = Excon.new('http://geemus.com')
get_response = connection.get
post_response = connection.post(:path => '/foo')
delete_response = connection.delete(:path => '/bar')

connection = Excon.new('http://geemus.com', :persistent => true)

connection = Excon.new('http://geemus.com')
connection.get
connection.get(:persistent => true)
connection.get(:persistent => true)
connection.get

connection = Excon.new('http://geemus.com', :persistent => true)
connection.get
connection.get(:persistent => false)
connection.get(:persistent => false)
connection.get
connection.get

connection = Excon.new('http://geemus.com/', :debug_request => true, :debug_response => true)

Excon.get('http://geemus.com', :headers => {'Authorization' => 'Basic 0123456789ABCDEF'})
connection.get(:headers => {'Authorization' => 'Basic 0123456789ABCDEF'})

connection = Excon.new('http://geemus.com/')
connection.get(:query => {:foo => 'bar'})

Excon.post('http://geems.com',
    :body => 'language=ruby&class=fog',
    :headers => { "Content-Type" => "application/x-www-form-urlencoded" })
    
Excon.post('http://geemus.com',
  :body => URI.encode_www_form(:language => 'ruby', :class => 'fog'),
  :headers => { "Content-Type" => "application/x-www-form-urlencoded" })

connection.request(:method => :get)
connection.request(:method => 'GET')
connection.request(:expects => [200, 201], :method => :get)
connection.request(:idempotent => true)
connection.request(:idempotent => true, :retry_limit => 6)
connection.request(:idempotent => true, :retry_limit => 6, :retry_interval => 5)
connection.request(:read_timeout => 360)
connection.request(:write_timeout => 360)
connection = Excon.new('http://geemus.com/', :tcp_nodelay => true)
connection = Excon.new('http://geemus.com/', :connect_timeout => 360)
connection = Excon.new('http://geemus.com/', :nonblock => false)
connection = Excon.new('http://username:password@secure.geemus.com')
connection = Excon.new('http://secure.geemus.com',
 :user => 'username', :password => 'password')
require 'addressable/uri'
connection = Excon.new('http://geemus.com/', uri_parser: Addressable::URI)

connection = Excon.new('http://geemus.com/', :omit_default_port => true)
connection = Excon.new('http://geemus.com/', :headers => { "Accept-Encoding" => "gzip" })
Excon.defaults[:ssl_verify_peer] = false
connection = Excon.new('https://...')

file = File.open('data')
chunker = lambda do
  file.read(Excon.defaults[:chunk_size]).to_s
end
Excon.post('http://geemus.com', :request_block => chunker)
file.close

connection = Excon.new('http://geemus.com/')
connection.requests([{:method => :get}, {:method => :get}])

large_array_of_requests = [{:method => :get, :path => 'some_path'}, { ... }]
connection.batch_requests(large_array_of_requests)

streamer = lambda do |chunk, remaing_bytes, total_bytes|
  puts chunk
  puts "Remaining: #{remaining_bytes.to_f / total_bytes}%"
end
Excon.get('http://geemus.com', :response_block => streamer)

connection = Excon.new('http://geemus.com', :proxy => 'http://my.proxy:3128')
connection.request(:method => 'GET')
Excon.get('http:/geemus.com', :proxy => 'http://my.proxy:3128')

connection = Excon.new('http://geemus.com', :reuseaddr => true)
connection.gte
s = Socket.new(Socket::AF_INET, Socket::SOCK_STREAM, 0)
s.setsockopt(Socket::SQL_SOCKET, Socket::SO_REUSEADDR, true)
if defined?(Socket::SO_REUSEPORT)
  s.setsockopt(Socket::SQL_SOCKET, Socket::SO_REUSEPORT, true)
end
s.bind(Socket.pack_sockaddr_in(connection.local_port, connection.local_address))
s.connect(Socket.pack_sockaddr_in(80, '1.2.3.4'))
puts s.read
s.close

connection = Excon.new('unix:///', :socket => '/tmp/unicorn.sock')
connection.request(:method => :get, :path => '/ping')
Excon.get('unix:///ping', :socket => '/tmp/unicorn.sock')

connection = Excon.new('http://example.com', :mock => true)
connection.request(:method => :get, :path => 'example', :mock => true)

Excon.stub({}, {:body => 'body', :status => 200})
Excon.stub({}, lambda (|request_params| {:body => request_params[:body], :status => 200}))

connection = Excon.new('http://example.com', :mock => true, :allow_unstubbed_request => true)

Excon.unstub({})
Excon.stub.clear

config.after(:each) do
  Excon.stubs.clear
end

config.before(:all) do
  Excon.defaults[:mock] = true
  Excon.stub({}, {:body => 'Fallback', :status => 200})
end

connection = Excon.new(
  'http://geemus.com',
  :instrumentor => ActiveSupport::Notifications
)

ActiveSupport::Notifications.subscribe(/excon/) do |*args|
  puts "Excon did stuff!"
end

connection = Excon.new(
  'http://geemus.com',
  :instrumentor => ActiveSupport::Notifications,
  :instrumentor_name => 'my_app'
)

class ExconToRailsInstrumentor
  def self.instrument(name, datum, &block)
    namespace, *event = name.split(".")
    rails_name = [event, namespace].flatten.join(".")
    ActiveSupport::Notifications.instrument(rails_name, datum, &block)
  end
end

class SimpleInstrumentor
  class << self
    attr_accessor :events
    def instrument(name, params = {}, &block)
      puts "#{name} just happened."
      yield if block_given?
    end
  end
end

connection = Excon.new('http://example.com',
                       client_cert: 'mycert.pem',
                       client_key: 'mycert.key',
                       client_key_pass: 'my pass phrase')
                       
client_cert_data = File.load 'mycert.pem'
client_key_data = File.load 'mycert.key'

connection = Excon.new('https://example.com',
                       client_cert_data: client_cert_data,
                       client_key_data: client_key_data)
                       
                       
Excon.defaults[:ssl_ca_path] = '/path/to/certs'
Excon.defaults[:ssl_verify_perr] = false

```
