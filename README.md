# python-whatsapp
A Python Client Library for WhatsApp.

The initial version of the protocol has been written with help from
[venomous0x's PHP Code](https://github.com/venomous0x/WhatsAPI), later versions
are mostly based on the on the code in the official Android App.

## Dependencies
The Client uses the [pbkdf2 library](https://www.dlitz.net/software/python-pbkdf2/)
written by Dwayne C. Litzenberger, which you can install using `pip install pbkdf2`.

## Usage
The API is callback driven and very easy to use. See below for a simple example.

```
import whatsappy

# Connecting
whatsapp = whatsappy.Client(number=<number>, secret=<secret>, nickname=<nickname>)
whatsapp.login()

# Callback
def on_message(node):
	message = node.child("body").data
    sender = node["from"]
    
    # Print response to terminal
    print "%s: %s" % (sender, message)
    
    # Reply
    whatsapp.message(receiver, message)

# Register callback
whatsapp.register_callbacks(
    TextMessageCallback(on_message, single=True, group=True, offline=True)
)
```

The secret is the password generated by WhatsApp. IMEI, MAC solutions do not work
anymore. It should be the raw secret, not encoded in Base64. This API does NOT 
provide any means of retrieving a secret from WhatsApp.

The interactive shell is not working at this moment.

## License
Released under the MIT License

Copyright (C) 2012 Paul Hooijenga  
Copyright (C) 2013 Bas Stottelaar

Permission is hereby granted, free of charge, to any person obtaining a copy of
this software and associated documentation files (the "Software"), to deal in
the Software without restriction, including without limitation the rights to
use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies
of the Software, and to permit persons to whom the Software is furnished to do
so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS
FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR
COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER
IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN
CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.
