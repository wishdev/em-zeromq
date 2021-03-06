# em-zeromq #

Low level event machine support for ZeroMQ

## Description: ##

This seems to work fine, no memory leaks, and it runs fast.
It may not be perfect though, and the API is extremely minimal, just the bare minumum
to make ZeroMQ work with EventMachine.

## Using: ##

You must use either rubinius, jruby, or 1.9.x. 1.8.7 does not work with libzmq.

If you use 1.9.x, be sure to install the ffi gem first.

For all rubies install ffi-rzmq and eventmachine as well.

This only works with ZeroMQ 2.1.x which is still unreleased
Build+Install ZeroMQ 2.1 from HEAD ( https://github.com/zeromq/zeromq2 ) 

Run the specs, see specs for examples

Want to help out? Ask!

## Example ##
    require 'rubygems'
    require 'em-zeromq'
        
    Thread.abort_on_exception = true

    class EMTestPullHandler
      attr_reader :received
      def on_readable(socket, messages)
        messages.each do |m|
          puts m.copy_out_string
        end
      end
    end
    class EMTestPushHandler
      attr_accessor :connection
      attr_reader   :queue
      
      def initialize
        @queue = []
      end
       
      def on_writable(socket)
        @queue.each do |item|
          socket.send_string item, ZMQ::NOBLOCK
        end
        connection.deregister_writable
      end
    end

    EM.run do
      ZCTX  = ZMQ::Context.new 1
      send_queue = []


      push_handler = EMTestPushHandler.new
      push = EM::ZeroMQ.create ZCTX, ZMQ::PUSH, :bind, 'tcp://127.0.0.1:2091', push_handler
      push_handler.connection = push
      
      
      pull = EM::ZeroMQ.create ZCTX, ZMQ::PULL, :connect, 'tcp://127.0.0.1:2091', EMTestPullHandler.new
      pull.register_readable
          
      EM::PeriodicTimer.new(1) do
        puts '.'
        push_handler.queue << "Test message #{Time.now}"
        push.register_writable
      end
    end

## License: ##

(The MIT License)

Copyright (c) 2011

Permission is hereby granted, free of charge, to any person obtaining
a copy of this software and associated documentation files (the
'Software'), to deal in the Software without restriction, including
without limitation the rights to use, copy, modify, merge, publish,
distribute, sublicense, and/or sell copies of the Software, and to
permit persons to whom the Software is furnished to do so, subject to
the following conditions:

The above copyright notice and this permission notice shall be
included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED 'AS IS', WITHOUT WARRANTY OF ANY KIND,
EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF
MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT.
IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY
CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT,
TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE
SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.
