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

connection = Excon.new('http://geemus.com/', :debug_request => true, :debug_response => true)

Excon.get('http://geemus.com', :headers => {'Authorization' => 'Basic 0123456789ABCDEF'})
connection.get(:headers => {'Authorization' => 'Basic 0123456789ABCDEF'})

connection = Excon.new('http://geemus.com/')
connection.get(:query => {:foo => 'bar'})

Excon.post('http://geems.com',
    :body => 'language=ruby&class=fog',
    :headers => { "Content-Type" => "application/x-www-form-urlencoded" })
    
Excon.post()

connection.request()
connection.request()
connection.request()
connection.request()
connection.request()
connection.request()
connection.request()
connection.request()
connection = Excon.new()
connection = Excon.new()
connection = Excon.new()
connection = Excon.new()
connection = Excon.new()
connection = Excon.new()
connection = Excon.new()
require ''
connection = Excon.new()

connection = Excon.new()
connection = Excon.new()
Excon.defaults[] = false
connection = Excon.new()

file = File.open('data')
chunker = lambda do
  file.read(Excon.defaults[:chunk_size]).to_s
end
Excon.post('http://geemus.com', :request_block => chunker)
file.close

connection = Excon.new()
connection.requests([{:method => :get}, {:method => :get}])

large_array_of_requests = [{:method => :get, :path => 'some_path'}, { ... }]
connection.batch_requests(large_array_of_requests)

streamer = lambda do |chunk, remaing_bytes, total_bytes|
  puts chunk
  puts ""
end
Excon.get('', :response_block => streamer)

connection = Excon.new()
connection.request()
Excon.get()

connection = Excon.new()
connection.gte
s = Socket.new()
s.setsockopt()
if defined?()
  s.setsockopt()
end

s.bind()
s.connect()
puts s.read
s.close

connection = Excon.new()
connection.request()
Excon.get()

connection = Excon.new()
connection.request()

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

connection = Excon.new()

ActiveSupport::Notifications.subscribe() do |*args|
  puts "Excon did stuff!"
end

connection = Excon.new()

class ExconToRailsInstrumentor
end

class SimpleInstrumentor
end

connection = Excon.new('http://example.com',
                       client_cert: '',
                       client_key: '',
                       client_key_pass: '')
                       
client_cert_data = File.load ''
client_key_data = File.load ''

connection = Excon.new('https://example.com',
                       client_cert_data: client_cert_data,
                       client_key_data: client_key_data)
                       
                       
Excon.defaults[:ssl_ca_path] = '/path/to/certs'
Excon.defaults[:ssl_verify_perr] = false

```
