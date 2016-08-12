## OSLP Documentation


## The Open Street Light Protocol

The OSLP is a lightweight message based protocol. 
OSLP uses [Google Protocol Buffers](https://developers.google.com/protocol-buffers/?hl=en) and is used for communication with SSLD devices (and device simulators). It is defined as a contract/interface. The interface defines datatypes and messages which use those datatypes.
Google Protocol Buffers is used to generate the protocol implementations for Java (for the platform) and C/C++ (for the SSLD devices).

Open street light protocol does not use ASN.1 but Google Protocol Buffers. The main reason for this is the lack of a good quality free ASN.1 compiler for Java or C. Google Protocol Buffers offers a fast and free compiler for Java and C which produces small message sizes.

## Protocol security
* Public/private keypair
* Signing of messages through Elliptic Curve DSA 256 bit
** Integrity of the message is ensured 
** Sender identity is ensured
** No encryption, because content is not confidential
* Replay attack prevention

### OSLP v0.5.1

The protobuf contract for [OSLP v0.5.1](./oslp/v0.5.1/oslp.proto.v0.5.1.md).
For v0.5.1 port number 12121 is used.

### OSLP v0.6.0

The protobuf contract for [OSLP v0.6.0](./oslp/v0.5.1/oslp.proto.v0.6.0.md).
For v0.6.0 port number 12122 is used.

### OSLP Envelope

The requests and responses are sent using an OSLP envelope. This structure contains the following fields: securityKey, sequenceNumber, deviceId and payloadMessage. The first 3 field are byte arrays, the payloadMessage is a protobuf type which is serializable.

``` java
class OslpEnvelope {
    /**
     * Length of the security hash.
     * Length for ECDSA is 71 or 72 or 73 bytes.
     * Length for RSA is 128 bytes.
     */
    public static final int SECURITY_KEY_LENGTH = 128;

    /**
     * Length of the sequence number.
     */
    public static final int SEQUENCE_NUMBER_LENGTH = 2;

    /**
     * Length of the manufacturer id.
     */
    public static final int MANUFACTURER_ID_LENGTH = 2;

    /**
     * Length of the device id.
     */
    public static final int DEVICE_ID_LENGTH = 10;

    /**
     * Length of the length.
     */
    public static final int LENGTH_INDICATOR_LENGTH = 2;

    /**
     * Buffer for security key bytes.
     */
    public byte[] securityKey = new byte[SECURITY_KEY_LENGTH];

    /**
     * Buffer for sequence number bytes.
     */
    public byte[] sequenceNumber = new byte[SEQUENCE_NUMBER_LENGTH];

    /**
     * Buffer for deviceid bytes.
     */
    public byte[] deviceId = new byte[DEVICE_ID_LENGTH + MANUFACTURER_ID_LENGTH];

    /**
     * Buffer for OSLP payload.
     */
    public Message payloadMessage;
}
```