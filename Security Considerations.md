# Security Considerations

This section is modeled after the template described in Section 3.7.1 of [RFC9907].

The “ietf-fgotn-topology”, “ietf-fgotn-tunnel” and “ietf-fgotn-types” YANG modules define data models that are designed to be accessed via YANG-based management protocols, such as NETCONF [RFC6241] and RESTCONF [RFC8040].  These protocols have to use a secure transport layer (e.g., SSH [RFC4252], TLS [RFC8446], and QUIC [RFC9000]) and have to use mutual authentication. in this document can be accessed via the RESTCONF protocol defined in [RFC8040], or maybe via the NETCONF protocol [RFC6241].

The Network Configuration Access Control Model (NACM) [RFC8341] provides the means to restrict access for particular NETCONF or RESTCONF users to a preconfigured subset of all available NETCONF or RESTCONF protocol operations and content.

There are a number of data nodes defined in “ietf-fgotn-topology” YANG module that are writable/creatable/deletable (i.e., config true, which is the default). These data nodes can be considered sensitive or vulnerable in some network environments.  Write operations (e.g., edit-config) to these data nodes without proper protection can have a negative effect on network operations. Specifically, the following subtrees and data nodes have particular sensitivities/vulnerabilities:

* "/nw:networks/nw:network/nt:link/tet:te/tet:te-link-attributes/tet:label-restrictions/tet:label-restriction/fgotnt:fgts-range"

This subtree specifies the configurations of fgOTN technology-specific label range information under any occurrence of the fgOTN links tet:te-label-restriction container, as defined in [RFC8795] (e.g., "/nw:networks/nw:network/nt:link/tet:te/tet:te-link-attributes/tet:label-restrictions/tet:label-restriction/fgotnt:fgts-range").  By configuring, removing or modifying the fgOTN label attributes, a malicious attacker may cause fgOTN traffic to be disabled or misrouted. Such traffic changes may also affect the traffic on the surrounding fgOTN nodes and fgOTN links in this fgOTN topology and the connected fgOTN topologies.

Some of the readable data nodes in this YANG module may be considered sensitive or vulnerable in some network environments. It is thus important to control read access (e.g., via get, get-config, or notification) to these data nodes. Specifically, the following subtrees and data nodes have particular sensitivities/ vulnerabilities:

*  "/nw:networks/nw:network/nt:link/tet:te/tet:te-link-attributes/tet:label-restrictions/tet:label-restriction/fgotnt:fgts-range"

This subtree specifies the configurations of fgOTN technology-specific label range information under any occurrence of the fgOTN link, as defined in [RFC8795] (e.g., "/nw:networks/nw:network/nt:link/tet:te/tet:te-link-attributes/tet:label-restrictions/tet:label-restriction/fgotnt:fgts-range").  Unauthorized access to this data node can disclose the state information of fgOTN links and link termination points.

There are a number of data nodes defined in “ietf-fgotn-tunnel” YANG module that are writable/creatable/deletable (i.e., config true, which is the default). These data nodes can be considered sensitive or vulnerable in some network environments.  Write operations (e.g., edit-config) to these data nodes without proper protection can have a negative effect on network operations. Specifically, the following subtrees and data nodes have particular sensitivities/vulnerabilities:

*  "/te:te/te:tunnels/te:tunnel/te:te-bandwidth/te:technology/otn-tnl:otn/otn-tnl:otn-bandwidth/fgotn-tnl:fgoduflex"

This node is represents the bandwidth of the fgOTN tunnel, as described in Section 5.2. By configuring the fgOTN bandwidth attributes, an attacker may create an unauthorized fgOTN traffic path. By removing or modifying it, a malicious attacker may cause fgOTN traffic to be disabled or misrouted. Such traffic changes may also affect the traffic on the surrounding fgOTN nodes and fgOTN links in this fgOTN topology and the connected fgOTN topologies.

*  "fgotn-tnl:fgts-numbers"
This node specifies the fgTS information on inter-domain ports of the routing path under any occurrence of the tet:te-label container, as defined in [I-D.ietf-teas-yang-te] (e.g., "/te:te/te:tunnels/te:tunnel/te:primary-paths/te:primary-path/te:explicit-route-objects/te:route-object-include-exclude/te:type/te:label/te:label-hop/te:te-label/te:technology/otnt:otn/otnt:otn-label/fgotn-tnl:fgts-numbers"). By configuring, removing or modifying the fgts attributes, a malicious attacker may cause fgOTN traffic to be disabled or misrouted.

Some of the readable data nodes in this YANG module may be considered sensitive or vulnerable in some network environments. It is thus important to control read access (e.g., via get, get-config, or notification) to these data nodes. Specifically, the following subtrees and data nodes have particular sensitivities/vulnerabilities:

*  "/te:te/te:tunnels/te:tunnel/te:te-bandwidth/te:technology/otn-tnl:otn/otn-tnl:otn-bandwidth/fgotn-tnl:fgoduflex"
This node is represents the bandwidth of the fgOTN tunnel, as described in Section 5.2. Unauthorized access to this data node can disclose the fgOTN bandwidth information of fgOTN tunnels and LSPs.

*  "fgotn-tnl:fgts-numbers"
This node specifies the fgTS information on inter-domain ports of the routing path under any occurrence of the tet:te-label container, as defined in [I-D.ietf-teas-yang-te] (e.g., "/te:te/te:tunnels/te:tunnel/te:primary-paths/te:primary-path/te:explicit-route-objects/te:route-object-include-exclude/te:type/te:label/te:label-hop/te:te-label/te:technology/otnt:otn/otnt:otn-label/fgotn-tnl:fgts-numbers"). Unauthorized access to this data node can disclose the state information of fgOTN tunnels and LSPs.

The “ietf-fgotn-topology” and “ietf-fgotn-tunnel” YANG modules does not define RPC operations.

The “ietf-fgotn-types” YANG module defines fgODUflex types. The nodes are intended to be reused by other YANG modules. The module by itselft does not expose any data nodes that are writable, data nodes that contain read-only state, or RPCs. As such, there are no additional security issues related to the YANG module that need to be considered.

This YANG module uses groupings from other YANG modules that define nodes that may be considered sensitive or vulnerable in network environments. Refer to the Security Considerations of [I-D.ietf-ccamp-layer1-types] for information as to which nodes may be considered sensitive or vulnerable in network environments.

Finally, the YANG module described in this document augments the  "ietf-otn-topology" YANG module [I-D.ietf-ccamp-otn-topo-yang] and "ietf-otn-tunnel" YANG module [I-D.ietf-ccamp-otn-tunnel-model] by adding data nodes. The security considerations for the subtrees described in those drafts apply equally to the new data nodes that this module adds.

