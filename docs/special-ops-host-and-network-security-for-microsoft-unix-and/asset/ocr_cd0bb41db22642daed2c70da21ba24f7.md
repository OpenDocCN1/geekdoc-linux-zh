# Chapter 17 • Architecting the Human Factor

There are two primary categories that need to be addressed in order to ensure a successful and secure remote access implementation. The first is organizational, involving formal coordination of requests and approvals, and documentation of the same. The second is technical, pertaining to the selection and configuration of the remote access gateway, and the implementation of individual requests.

# Organizational VPN Access Procedures

The organizational aspect of your remote access solution should be a well-defined process of activity commencing when the first request is made to permit remote access, following through the process of activation and periodically verifying compliance after the request has been granted. The following steps provide some suggestions for developing this phase of a request:

+   1. Prepare a template to be completed by the internal requester of remote access. The questions this document should address include following:
* **Justification for remote access request** Why does the remote party need access? This open-ended question will help identify situations where remote access may not really be necessary, or where access can be limited in scope or duration.
* **Anticipated frequency of access** How frequently will this connection be used? If access is anticipated to be infrequent, can the account be left disabled between users?
* **Resources required for task** What system(s) does the remote client need to access? What specific services will the remote client require? It if your remote access policy restricts the types of service provided to third-party entities, in which case you provide a checklist of the service types available and provide space for justification.
* **Authentication and access-control** What form of authentication and access-control is in place on the target systems? It should be made clear to the internal requesting party that once access is approved, the administrator(s) of the hosts being made available via VPN are responsible for ensuring that the host cannot be used as a proxy to gain additional network access.