# Nostr network stack (nns) nip - "Virtual Relays"

This nip should introduce a way of communication between a "Virtual Client" with a "Virtual Relay", both identified by a nostr-npub, over nostr events. 


The "Virtual Relay" creates a nostr-nsec/npub identity, or is attributed with an existing one. It publishes a kind `10112`-event with relays on which it listens to nns-requests and sends nns-responses.
The kind `10112`-event follows the structure of NIP65 and NIP51 and signals that the pukey is reachable for nns-communication there.

The user of the "Virtual Relay" references the "Virtual Relay" in events that need a `r`-tag (e.g. kind `10002`), with ["r", "nns://npu1..."].


The nns-event has the following pattern:

~~~
{
  "id": <32-bytes lowercase hex-encoded sha256 of the serialized note data>,
  "pubkey": <32-bytes lowercase hex-encoded public key of the sender of the message (e.g. "Virtual Relay" or "Virtual Client">,
  "kind": 27901, // as defined in NIP-01 an ephemeral kind-number is used for this event-type
  "tags": [
    ["p", <32-bytes lowercase hex-encoded public key of the receiver of the message (e.g. "Virtual Relay" or "Virtual Client">],
  ]
  "content": nip44_encrypt({
    <messages between client and relay as defined in e.g. NIP01, NIP77, ... in the nostr-protocol>
  }),
  "sig": <64-bytes lowercase hex of the signature of the sha256 hash of the serialized event data, which is the same as the "id" field>
}
~~~

The events should be treated as ephemeral by relays.
