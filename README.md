# UbSub - Internet of Things (IoT)

C++ implementation of ubsub's UDP protocol for secure and reliable bidirectional communication for embedded devices.

# Usage

## Simple Unix Example

```cpp
#include <iostream>
#include <unistd.h>
#include "ubsub.h"

Ubsub client("MyUserId", "MyUserSecret");

void myMethod(const char* arg) {
  std::cout << "RECEIVED: " << arg << std::endl;
}

int main() {
  std::cout << "Hi there" << std::endl;

  if (!client.connect()) {
    std::cout << "Failed to connect before timeout" << std::endl;
  }

  client.listenToTopic("testy", myMethod);

  client.publishEvent("Byg2kKB3SZ", "HJ3ytS3SW", "Hi there");

  while(true) {
    client.processEvents(); // Need to call this to process incoming events and managed items
    usleep(5 * 1000);
  }

  return 0;
}

```

## Simple Arduino/Particle Example
```cpp
#include <iostream>
#include <unistd.h>
#include "ubsub.h"

Ubsub client("MyUserId", "MyUserSecret");

void myMethod(const char* arg) {
  // Called method with argument
}

void setup() {
  while (!client.connect()) {
    // Attempting connect
  }

  client.listenToTopic("testy", myMethod);
  client.publishEvent("Byg2kKB3SZ", "HJ3ytS3SW", "Hi there");
}

void loop() {
  // Do whatever else you need to do

  // Need to call this to process incoming events and managed items
  client.processEvents();
}
```

# Compatability

 * Unix/Linux
 * Arduino
 * Particle
 * ESP8266 Boards

# Third Party

## CryptoSuite

Sha256 implementation is from [Cathedrow/Cryptosuite](https://github.com/Cathedrow/Cryptosuite) with small modifications
for compatibility.

## Salsa20

Salsa Implementation from: https://github.com/alexwebr/salsa20

# License

Copyright (c) 2017 Christopher LaPointe (ubsub.io)

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.

