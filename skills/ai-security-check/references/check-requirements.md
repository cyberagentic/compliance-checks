# AI Security Quick Check — Requirements Catalog (11 Check Points)

## How to use this reference

Each check point groups controls from ISO/IEC 27001:2022 and/or ISO/IEC 42001:2023 that must be assessed against the AI system's security documentation. The controls themselves are the review criteria — each control shall be checked individually against the document.

Where controls from both standards overlap, they appear in a single row with combined sources and descriptions.

The check uses a 3-level traffic light scale:

- **🟢 GREEN** — Requirement met
- **🟡 YELLOW** — Action needed — topic addressed but incomplete or too generic
- **🔴 RED** — Critical — topic missing or not discernibly regulated

---

## AIS-01 — Asset Management

| Control Nr. | Quelle | Control Name | Beschreibung |
|-------------|--------|--------------|--------------|
| 5.9 | ISO 27001 | Inventory of information and other associated assets | An inventory of information and other associated assets, including owners, shall be developed and maintained. |
| 5.12 | ISO 27001 | Classification of information | Information shall be classified according to the information security needs of the organization based on confidentiality, integrity, availability and relevant interested party requirements. |
| 5.13 | ISO 27001 | Labelling of information | An appropriate set of procedures for information labelling shall be developed and implemented in accordance with the information classification scheme adopted by the organization. |

### Assessment Criteria

- **🟢 GREEN:** All controls addressed and adequately described.
- **🟡 YELLOW:** Controls partially addressed — some topics covered but incomplete or too generic.
- **🔴 RED:** Controls not addressed — topic missing or not discernibly regulated.

---

## AIS-02 — Access Control

| Control Nr. | Quelle | Control Name | Beschreibung |
|-------------|--------|--------------|--------------|
| 5.15 | ISO 27001 | Access control | Rules to control physical and logical access to information and other associated assets shall be established and implemented based on business and information security requirements. |
| 5.16 | ISO 27001 | Identity management | The full life cycle of identities shall be managed. |
| 5.17 | ISO 27001 | Authentication information | Allocation and management of authentication information shall be controlled by a management process, including advising personnel on appropriate handling of authentication information. |
| 5.18 | ISO 27001 | Access rights | Access rights to information and other associated assets shall be provisioned, reviewed, modified and removed in accordance with the organization's topic-specific policy on and rules for access control. |
| 8.2 | ISO 27001 | Privileged access rights | The allocation and use of privileged access rights shall be restricted and managed. |
| 8.3 | ISO 27001 | Information access restriction | Access to information and other associated assets shall be restricted in accordance with the established topic-specific policy on access control. |
| 8.4 | ISO 27001 | Access to source code | Read and write access to source code, development tools and software libraries shall be appropriately managed. |
| 8.5 | ISO 27001 | Secure authentication | Secure authentication technologies and procedures shall be implemented based on information access restrictions and the topic-specific policy on access control. |

### Assessment Criteria

- **🟢 GREEN:** All controls addressed and adequately described.
- **🟡 YELLOW:** Controls partially addressed — some topics covered but incomplete or too generic.
- **🔴 RED:** Controls not addressed — topic missing or not discernibly regulated.

---

## AIS-03 — Cryptography

| Control Nr. | Quelle | Control Name | Beschreibung |
|-------------|--------|--------------|--------------|
| 8.24 | ISO 27001 | Use of cryptography | Rules for the effective use of cryptography, including cryptographic key management, shall be defined and implemented. |

### Assessment Criteria

- **🟢 GREEN:** All controls addressed and adequately described.
- **🟡 YELLOW:** Controls partially addressed — some topics covered but incomplete or too generic.
- **🔴 RED:** Controls not addressed — topic missing or not discernibly regulated.

---

## AIS-04 — Operations Security

| Control Nr. | Quelle | Control Name | Beschreibung |
|-------------|--------|--------------|--------------|
| 8.6 / A.4.5 | ISO 27001 / ISO 42001 | Capacity management / System and computing resources | 8.6: The use of resources shall be monitored and adjusted in line with current and expected capacity requirements. A.4.5: As part of resource identification, the organization shall document information about the system and computing resources utilized for the AI system. |
| 8.7 | ISO 27001 | Protection against malware | Protection against malware shall be implemented and supported by appropriate user awareness. |
| 8.8 | ISO 27001 | Management of technical vulnerabilities | Information about technical vulnerabilities of information systems in use shall be obtained, the organization's exposure to such vulnerabilities shall be evaluated and appropriate measures shall be taken. |
| 8.9 | ISO 27001 | Configuration management | Configurations, including security configurations, of hardware, software, services and networks shall be established, documented, implemented, monitored and reviewed. |
| 8.10 | ISO 27001 | Information deletion | Information stored in information systems, devices or in any other storage media shall be deleted when no longer required. |
| 8.11 | ISO 27001 | Data masking | Data masking shall be used in accordance with the organization's topic-specific policy on access control and other related topic-specific policies, and business requirements, taking applicable legislation into consideration. |
| 8.12 | ISO 27001 | Data leakage prevention | Data leakage prevention measures shall be applied to systems, networks and any other devices that process, store or transmit sensitive information. |
| 8.13 | ISO 27001 | Information backup | Backup copies of information, software and systems shall be maintained and regularly tested in accordance with the agreed topic-specific policy on backup. |
| 8.15 / A.6.2.8 | ISO 27001 / ISO 42001 | Logging / AI system recording of event logs | 8.15: Logs that record activities, exceptions, faults and other relevant events shall be produced, stored, protected and analysed. A.6.2.8: The organization shall determine at which phases of the AI system life cycle, record keeping of event logs should be enabled, but at the minimum when the AI system is in use. |
| 8.16 / A.6.2.6 | ISO 27001 / ISO 42001 | Monitoring activities / AI system operation and monitoring | 8.16: Networks, systems and applications shall be monitored for anomalous behaviour and appropriate actions taken to evaluate potential information security incidents. A.6.2.6: The organization shall define and document the necessary elements for the ongoing operation of the AI system. At the minimum, this should include system and performance monitoring, repairs, updates and support. |

### Assessment Criteria

- **🟢 GREEN:** All controls addressed and adequately described.
- **🟡 YELLOW:** Controls partially addressed — some topics covered but incomplete or too generic.
- **🔴 RED:** Controls not addressed — topic missing or not discernibly regulated.

---

## AIS-05 — Communications Security

| Control Nr. | Quelle | Control Name | Beschreibung |
|-------------|--------|--------------|--------------|
| 5.14 | ISO 27001 | Information transfer | Information transfer rules, procedures, or agreements shall be in place for all types of transfer facilities within the organization and between the organization and other parties. |
| 8.20 | ISO 27001 | Networks security | Networks and network devices shall be secured, managed and controlled to protect information in systems and applications. |
| 8.21 | ISO 27001 | Security of network services | Security mechanisms, service levels and service requirements of network services shall be identified, implemented and monitored. |
| 8.22 | ISO 27001 | Segregation of networks | Groups of information services, users and information systems shall be segregated in the organization's networks. |

### Assessment Criteria

- **🟢 GREEN:** All controls addressed and adequately described.
- **🟡 YELLOW:** Controls partially addressed — some topics covered but incomplete or too generic.
- **🔴 RED:** Controls not addressed — topic missing or not discernibly regulated.

---

## AIS-06 — System Acquisition, Development & Maintenance

| Control Nr. | Quelle | Control Name | Beschreibung |
|-------------|--------|--------------|--------------|
| 8.25 / A.6.1.3 / A.6.1.2 | ISO 27001 / ISO 42001 | Secure development life cycle / Processes for responsible AI system design and development / Objectives for responsible development of AI system | 8.25: Rules for the secure development of software and systems shall be established and applied. A.6.1.3: The organization shall define and document the specific processes for the responsible design and development of the AI system. A.6.1.2: The organization shall identify and document objectives to guide the responsible development AI systems, and take those objectives into account and integrate measures to achieve them in the development life cycle. |
| 8.26 / A.6.2.2 / A.6.2.3 | ISO 27001 / ISO 42001 | Application security requirements / AI system requirements and specification / Documentation of AI system design and development | 8.26: Information security requirements shall be identified, specified and approved when developing or acquiring applications. A.6.2.2: The organization shall specify and document requirements for new AI systems or material enhancements to existing systems. A.6.2.3: The organization shall document the AI system design and development based on organizational objectives, documented requirements and specification criteria. |
| 8.27 | ISO 27001 | Secure system architecture and engineering principles | Principles for engineering secure systems shall be established, documented, maintained and applied to any information system development activities. |
| 8.28 | ISO 27001 | Secure coding | Secure coding principles shall be applied to software development. |
| 8.29 / A.6.2.4 | ISO 27001 / ISO 42001 | Security testing in development and acceptance / AI system verification and validation | 8.29: Security testing processes shall be defined and implemented in the development life cycle. A.6.2.4: The organization shall define and document verification and validation measures for the AI system and specify criteria for their use. |
| 8.30 / A.10.3 | ISO 27001 / ISO 42001 | Outsourced development / Suppliers | 8.30: The organization shall direct, monitor and review the activities related to outsourced system development. A.10.3: The organization shall establish a process to ensure that its usage of services, products or materials provided by suppliers aligns with the organization's approach to the responsible development and use of AI systems. |
| 8.31 | ISO 27001 | Separation of development, test and production environments | Development, testing and production environments shall be separated and secured. |
| 8.32 / A.6.2.7 | ISO 27001 / ISO 42001 | Change management / AI system technical documentation | 8.32: Changes to information processing facilities and information systems shall be subject to change management procedures. A.6.2.7: The organization shall determine what AI system technical documentation is needed for each relevant category of interested parties, such as users, partners, supervisory authorities, and provide the technical documentation to them in the appropriate form. |

### Assessment Criteria

- **🟢 GREEN:** All controls addressed and adequately described.
- **🟡 YELLOW:** Controls partially addressed — some topics covered but incomplete or too generic.
- **🔴 RED:** Controls not addressed — topic missing or not discernibly regulated.

---

## AIS-07 — Supplier Relationships

| Control Nr. | Quelle | Control Name | Beschreibung |
|-------------|--------|--------------|--------------|
| 5.23 / A.6.2.5 | ISO 27001 / ISO 42001 | Information security for use of cloud services / AI system deployment | 5.23: Processes for acquisition, use, management and exit from cloud services shall be established in accordance with the organization's information security requirements. A.6.2.5: The organization shall document a deployment plan and ensure that appropriate requirements are met prior to deployment. |

### Assessment Criteria

- **🟢 GREEN:** All controls addressed and adequately described.
- **🟡 YELLOW:** Controls partially addressed — some topics covered but incomplete or too generic.
- **🔴 RED:** Controls not addressed — topic missing or not discernibly regulated.

---

## AIS-08 — Business Continuity

| Control Nr. | Quelle | Control Name | Beschreibung |
|-------------|--------|--------------|--------------|
| 8.14 | ISO 27001 | Redundancy of information processing facilities | Information processing facilities shall be implemented with redundancy sufficient to meet availability requirements. |

### Assessment Criteria

- **🟢 GREEN:** All controls addressed and adequately described.
- **🟡 YELLOW:** Controls partially addressed — some topics covered but incomplete or too generic.
- **🔴 RED:** Controls not addressed — topic missing or not discernibly regulated.

---

## AIS-09 — Resources for AI Systems

| Control Nr. | Quelle | Control Name | Beschreibung |
|-------------|--------|--------------|--------------|
| A.4.2 | ISO 42001 | Resource documentation | The organization shall identify and document relevant resources required for the activities at given AI system life cycle stages and other AI-related activities relevant for the organization. |
| A.4.3 | ISO 42001 | Data resources | As part of resource identification, the organization shall document information about the data resources utilized for the AI system. |
| A.4.4 | ISO 42001 | Tooling resources | As part of resource identification, the organization shall document information about the tooling resources utilized for the AI system. |
| A.4.6 | ISO 42001 | Human resources | As part of resource identification, the organization shall document information about the human resources and their competences utilized for the development, deployment, operation, change management, maintenance, transfer and decommissioning, as well as verification and integration of the AI system. |

### Assessment Criteria

- **🟢 GREEN:** All controls addressed and adequately described.
- **🟡 YELLOW:** Controls partially addressed — some topics covered but incomplete or too generic.
- **🔴 RED:** Controls not addressed — topic missing or not discernibly regulated.

---

## AIS-10 — Assessing Impacts of AI Systems

| Control Nr. | Quelle | Control Name | Beschreibung |
|-------------|--------|--------------|--------------|
| A.5.2 | ISO 42001 | AI system impact assessment process | The organization shall establish a process to assess the potential consequences for individuals or groups of individuals, or both, and societies that can result from the AI system throughout its life cycle. |
| A.5.3 | ISO 42001 | Documentation of AI system impact assessments | The organization shall document the results of AI system impact assessments and retain results for a defined period. |
| A.5.4 | ISO 42001 | Assessing AI system impact on individuals or groups of individuals | The organization shall assess and document the potential impacts of AI systems to individuals or groups of individuals throughout the system's life cycle. |

### Assessment Criteria

- **🟢 GREEN:** All controls addressed and adequately described.
- **🟡 YELLOW:** Controls partially addressed — some topics covered but incomplete or too generic.
- **🔴 RED:** Controls not addressed — topic missing or not discernibly regulated.

---

## AIS-11 — Data for AI Systems

| Control Nr. | Quelle | Control Name | Beschreibung |
|-------------|--------|--------------|--------------|
| A.7.2 | ISO 42001 | Data for development and enhancement of AI system | The organization shall define, document and implement data management processes related to the development of AI systems. |
| A.7.3 | ISO 42001 | Acquisition of data | The organization shall determine and document details about the acquisition and selection of the data used in AI systems. |
| A.7.4 | ISO 42001 | Quality of data for AI systems | The organization shall define and document requirements for data quality and ensure that data used to develop and operate the AI system meet those requirements. |
| A.7.5 | ISO 42001 | Data provenance | The organization shall define and document a process for recording the provenance of data used in its AI systems over the life cycles of the data and the AI system. |
| A.7.6 | ISO 42001 | Data preparation | The organization shall define and document its criteria for selecting data preparations and the data preparation methods to be used. |

### Assessment Criteria

- **🟢 GREEN:** All controls addressed and adequately described.
- **🟡 YELLOW:** Controls partially addressed — some topics covered but incomplete or too generic.
- **🔴 RED:** Controls not addressed — topic missing or not discernibly regulated.
