Column Name	                                                              Description
Timestamp	                                                                The time when the CAN message was recorded (in seconds).
Arbitration_ID	                                                          The identifier of the CAN message (usually in hexadecimal).
DLC                                                                       Data Length Code (number of bytes in the Data field).
Data	                                                                    The actual CAN message payload in hexadecimal format.
Class	                                                                    The label indicating if the message is Normal or an Attack.
SubClass	                                                                Further classification of the attack (e.g., DoS, Fuzzy, Spoofing).
abstime	                                                                  Absolute timestamp, converted from Timestamp into a human-readable datetime format.
monotime	                                                                Time elapsed since the first recorded CAN message.
aid_int	                                                                  The Arbitration_ID converted from hexadecimal to an integer.
y	                                                                        The target label (0 for Normal, 1 for Attack).
time_interval	                                                            Time difference between consecutive messages with the same Arbitration_ID.
datafield0 to datafield7	                                                Individual bytes extracted from the Data field (filled with -1 if missing).
entropy	                                                                  Shannon entropy of aid_int over a rolling window (used for anomaly detection).


The Data field in a CAN message contains payload bytes that carry the actual information. The DLC (Data Length Code) specifies how many bytes are present (from 0 to 8 bytes). Since some messages have fewer than 8 bytes, missing values are typically padded with -1.

How the Data Field is Processed
The Data field is originally in hexadecimal format (e.g., "5A 3C FF 01").

Each byte (2 hex characters) is converted into an integer.

If the message has fewer than 8 bytes, it is padded with -1.

Example 1: Data field with 4 bytes
Original Data	                                          Converted to datafield0-datafield7
"5A 3C FF 01"	                                          [90, 60, 255, 1, -1, -1, -1, -1]

Here,
"5A" → 90

"3C" → 60

"FF" → 255

"01" → 1

Missing values (-1) fill the remaining 4 slots.
