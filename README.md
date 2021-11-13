# Arithmetic_Coding

This project implements the lossless data compression technique called arithmetic encoding (AE). The project is simple and has just some basic features.

The project supports encoding the input as both a floating-point value and a binary code.

The project has a main module called pyae.py which contains a class called ArithmeticEncoding to encode and decode messages.


# Steps

To use the project, follow these steps:

    1-Import pyae
    2-Instantiate the ArithmeticEncoding Class
    3-Prepare a Message
    4-Encode the Message
    5-Get the binary code of the encoded message.
    6-Decode the Message
    

# Import pyae
The first step is to import the pyae module.

`import pyae`


# Instantiate the ArithmeticEncoding Class
Create an instance of the ArithmeticEncoding class. Its constructor accepts 2 arguments:

        frequency_table: The frequency table as a dictionary where key is the symbol and value is the frequency.
        save_stages: If True, then the intervals of each stage are saved in a list. Note that setting save_stages=True may cause memory overflow if the message is large
According to the following frequency table, the messages to be encoded/decoded must have only the 3 characters a, b, and c.
````
frequency_table = {"a": 2,
                   "b": 7,
                   "c": 1}

AE = pyae.ArithmeticEncoding(frequency_table=frequency_table,
                            save_stages=True)
````                           
                           
                           
                           
 # Prepare a Message
Prepare the message to be compressed. All the characters in this message must exist in the frequency table.

`original_msg = "abc"
`


# Encode the Message
Encode the message using the encode() method. It accepts the message to be encoded and the probability table. It returns the encoded message (single double value) and the encoder stages.

`encoded_msg, encoder , interval_min_value, interval_max_value = AE.encode(msg=original_msg, 
                                                                          probability_table=AE.probability_table)                                                                      
`


# Decode the Message
Decode the message using the decode() method. It accepts the encoded message, message length, and the probability table. It returns the decoded message and the decoder stages.

`decoded_msg, decoder = AE.decode(encoded_msg=encoded_msg, 
                                 msg_length=len(original_msg),
                                 probability_table=AE.probability_table)
`


# Example

The example.py script has an example that compresses the message abc using arithmetic encoding. The precision of the decimal data type is left to the default value 28 as it can encode the message abc without losing any information.

````
import pyae

# Example for encoding a simple text message using the PyAE module.
# This example returns the floating-point value in addition to its binary code that encodes the message. 

frequency_table = {"a": 2,
                   "b": 7,
                   "c": 1}

AE = pyae.ArithmeticEncoding(frequency_table=frequency_table,
                            save_stages=True)

original_msg = "abc"
print("Original Message: {msg}".format(msg=original_msg))

# Encode the message
encoded_msg, encoder , interval_min_value, interval_max_value = AE.encode(msg=original_msg, 
                                                                          probability_table=AE.probability_table)
print("Encoded Message: {msg}".format(msg=encoded_msg))

# Get the binary code out of the floating-point value
binary_code, encoder_binary = AE.encode_binary(float_interval_min=interval_min_value,
                                               float_interval_max=interval_max_value)
print("The binary code is: {binary_code}".format(binary_code=binary_code))

# Decode the message
decoded_msg, decoder = AE.decode(encoded_msg=encoded_msg, 
                                 msg_length=len(original_msg),
                                 probability_table=AE.probability_table)
decoded_msg = "".join(decoded_msg)
print("Decoded Message: {msg}".format(msg=decoded_msg))
print("Message Decoded Successfully? {result}".format(result=original_msg == decoded_msg))
````


The printed messages out of the code are:


```Original Message: abc
Encoded Message: 0.1729999999999999989175325511
The binary code is: 0.0010110
Decoded Message: abc
Message Decoded Successfully? True          
```


# Contact Us
* E-mail: 4eng.ash@gmail.com
* [GitHub](https://github.com/Shamakhi/)
