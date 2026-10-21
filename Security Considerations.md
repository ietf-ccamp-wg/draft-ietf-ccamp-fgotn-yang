# Security Considerations

This section is modeled after the template described in Section 3.7.1 of {{?RFC9907}}.

The "ietf-fgotn-topology", "ietf-fgotn-tunnel" and "ietf-fgotn-types" YANG modules define data models that are designed to be accessed via YANG-based management protocols, such as
Network Configuration Protocol (NETCONF) {{?RFC6241}} and RESTCONF {{?RFC8040}}.
These YANG-based management protocols (1) have to use a secure transport
layer (e.g., SSH {{?RFC4253}}, TLS {{?RFC9846}}, and
QUIC {{?RFC9000}}) and (2) have to use mutual authentication (e.g., for SSH, the SSH Authentication Protocol {{?RFC4252}}).

The Network Configuration Access Control Model (NACM) {{!RFC8341}} provides the means to restrict access for particular NETCONF or RESTCONF users to a preconfigured subset of all available NETCONF or
RESTCONF protocol operations and content.

There are a number of data nodes defined in these YANG modules that are writable/creatable/deletable (i.e., config true, which is the default).
All writable data nodes are likely to be reasonably sensitive or vulnerable in some network environments.
Write operations (e.g., edit-config) and delete operations to these data nodes without proper protection or authentication can have a negative effect on network operations.
The following subtrees and data nodes have particular sensitivities/vulnerabilities:

- "/nw:networks/nw:network/nt:link/tet:te/tet:te-link-attributes/tet:label-restrictions/tet:label-restriction/fgotnt:fgts-range"

> This subtree specifies the configurations of fgOTN technology-specific label range information for the fgOTN links. By configuring, removing or modifying the fgOTN label attributes, a malicious attacker may cause fgOTN traffic to be disabled or misrouted. Such traffic changes may also affect the traffic on the surrounding fgOTN nodes and fgOTN links in this fgOTN topology and the connected fgOTN topologies.

- "/te:te/te:tunnels/te:tunnel/te:te-bandwidth/te:technology/otn-tnl:otn/otn-tnl:otn-bandwidth/fgotn-tnl:fgoduflex-bandwidth"

> This data node represents the bandwidth of the fgOTN tunnel, as described in {{tunnel-bandwidth}}. By configuring the fgOTN bandwidth attributes, an attacker may create an unauthorized fgOTN traffic path. By removing or modifying it, a malicious attacker may cause fgOTN traffic to be disabled or misrouted.

- "fgotn-tnl:fgts-numbers"

> This data node specifies the fgTS information for the explicit route objects and computed path properties of fgOTN paths, under the corresponding occurrences of the tet:te-label container, as defined in {{!I-D.ietf-teas-yang-te}} (e.g., "/te:te/te:tunnels/te:tunnel/te:primary-paths/te:primary-path/te:explicit-route-objects/te:route-object-include-exclude/te:type/te:label/te:label-hop/te:te-label/te:technology/otnt:otn/otnt:otn-label/fgotn-tnl:fgts-numbers"). By configuring, removing or modifying the fgTS attributes, a malicious attacker may cause fgOTN traffic to be disabled or misrouted.

Some of the readable data nodes in these YANG modules may be considered sensitive or vulnerable in some network environments.
It is thus important to control read access (e.g., via get, get-config, or notification) to these data nodes.
Specifically, the following subtrees and data nodes have particular sensitivities/ vulnerabilities:

- "/nw:networks/nw:network/nt:link/tet:te/tet:te-link-attributes/tet:label-restrictions/tet:label-restriction/fgotnt:fgts-range"

> This subtree specifies the configurations of fgOTN technology-specific label range information for the fgOTN links. Unauthorized access to this subtree can disclose the state information of fgOTN links.

- "/te:te/te:tunnels/te:tunnel/te:te-bandwidth/te:technology/otn-tnl:otn/otn-tnl:otn-bandwidth/fgotn-tnl:fgoduflex"

> This data node represents the bandwidth of the fgOTN tunnel, as described in {{tunnel-bandwidth}}. Unauthorized access to this data node can disclose the fgOTN bandwidth information of fgOTN tunnels and LSPs.

- "fgotn-tnl:fgts-numbers"

> This data node specifies the fgTS information for the explicit route objects and computed path properties of fgOTN paths, under the corresponding occurrences of the tet:te-label container, as defined in {{!I-D.ietf-teas-yang-te}} (e.g., "/te:te/te:tunnels/te:tunnel/te:primary-paths/te:primary-path/te:explicit-route-objects/te:route-object-include-exclude/te:type/te:label/te:label-hop/te:te-label/te:technology/otnt:otn/otnt:otn-label/fgotn-tnl:fgts-numbers"). Unauthorized access to this data node can disclose the state information of fgOTN tunnels and LSPs.

These YANG modules do not define RPC operations.

Finally, the YANG modules described in this document augments the "ietf-otn-topology" YANG module {{!I-D.ietf-ccamp-otn-topo-yang}} and the "ietf-otn-tunnel" YANG module {{!I-D.ietf-ccamp-otn-tunnel-model}} by adding data nodes. The security considerations for the subtrees described in those drafts apply equally to the new data nodes that these modules add.
