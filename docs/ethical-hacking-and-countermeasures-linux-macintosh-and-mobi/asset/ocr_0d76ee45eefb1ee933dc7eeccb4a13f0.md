Memorandum of Agreement (MOA) or Memorandum of Understanding (MOU). The MOU or MOA specifies the network connections and authentication mechanisms to be used, the data to be shared, and the manner in which data should be protected both in transit and at rest. It may also address controls on vendors, subcontractors, and other third parties regarding the extent to which they have access to the system.

If the interenterprise application requires tag passwords to be shared across organizations, then the MOU or MOA should specify how these passwords will be generated, stored, and shared. The memorandum may specify IT security controls such as methods of authentication, access control, or encryption that participating organizations shall implement to protect the passwords.

**Benefits**: Having an MOA or MOU significantly reduces the potential for subsequent misunderstandings and security breaches. They enable signatories to communicate their respective security requirements while also realizing the benefits of the business partnership that led them to collaborate in the development and use of the RFID system.

**Weaknesses**: Monitoring an external organization’s enforcement of an agreement is difficult without full access to its systems and personnel, which is unlikely. As a result, violations may occur without detection. This risk can be mitigated with independent audits if signatories agree to hire third parties to conduct such audits.

# ## Minimizing Sensitive Data Stored on Tags

Control: Instead of placing sensitive data on tags, the data could be stored in a secure enterprise subsystem and retrieved using the tag’s unique identifier.

**Applicability**: Applications that use tags with on-board memory and process data that is either considered sensitive or could be combined with other data to infer sensitive information.

**Benefits**: Adversaries cannot obtain information from the tag through rogue scanning or eavesdropping. Data encryption and access control is often more cost effective if performed in the enterprise’s subsystem rather than in the RF subsystem.

**Weaknesses**: Adversaries can often obtain valuable information from the identifier alone. For example, knowledge of the EPC manager ID and object class bits in certain EPC formats may reveal the make and model of a tagged object concealed in a container. An adversary could target containers based on the perceived worth of their contents.

Additionally, placing data in the enterprise subsystem makes the availability of that data contingent on the availability of the network. Retrieving data over a network also introduces a small delay, which could be unacceptable for some applications.

# # Operational Controls

# ## Physical Access Control

Control: Physical access controls include fences, gates, walls, locked doors, turnstiles, surveillance cameras, and security guards. When the objective is to limit radio communication over a short distance, room walls or partitioned stalls might provide adequate protection if they are opaque to the relevant radio frequencies that the RF subsystem uses.

**Applicability**: All RFID implementations, except those in which RFID tags or other system components are in the public areas.

**Benefits**: Physical access controls limit the ability of an adversary to get close enough to RFID system components to compromise RFID data security or to modify, damage, or steal RFID system components. Physical security applies to all RFID subsystems. In the RF subsystem, the primary objective of the control is to prevent unauthorized radio communications. In the enterprise and interenterprise subsystems, the primary objective is to prevent physical access to the system components.

# ## Appropriate Placement of Tags and Readers

Control: RFID system equipment can be placed to minimize unnecessary electromagnetic radiation. Tags and readers can be kept away from:

+   * Fuel, ordnance, and other materials that could cause harm if exposed to the electromagnetic radiation
+   * Humans and sensitive products (e.g., blood, medicine) that might be harmed by sustained exposure to the RF subsystem radiation
+   * Metal and reflective objects that can modify and amplify signals in unintended and potentially harmful ways
+   * Legitimate radios with which the RF subsystem communication will cause interference