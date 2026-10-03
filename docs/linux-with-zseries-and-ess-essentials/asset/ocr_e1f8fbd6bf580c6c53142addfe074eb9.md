+   ► The ESS copy functions that fall within the *local copy* category are:
  – FlashCopy
  – Concurrent Copy

The ESS Copy Services copy functions can also be classified as either *dynamic* or *point-in-time*. Dynamic copy functions constantly update the secondary copy as applications make changes to the primary data source. Point-in-time copy functions provide an instantaneous copy or view of what the original data looked like at a specific point-in-time. For example, the Remote Copy functions listed above are all *dynamic*, while the local copy functions mentioned above are both *point-in-time*.

# 6.2 Peer-to-Peer Remote Copy (PPRC)

Peer-to-Peer Remote Copy (PPRC) is a synchronous remote data mirroring technology used primarily as part of a business continuance solution for protection against disk subsystem loss, or complete site failure. It is also used for remote migration of data and application workloads, and for off-site backups. It is a real-time copy technique that synchronously mirrors a *primary* set of volumes (that are being used by applications) onto a *secondary* set of volumes (see Figure 6-2). Typically, the secondary volumes will be on a different ESS located at a remote location some distance away from the application site. Mirroring is done at a logical volume level.

![](bbox=[0.22, 0.45, 0.9, 0.77])

Figure 6-2 Synchronous volume copy PPRC

PPRC is a hardware solution, thus it is application independent and the relevant hardware feature needs to be available on both the local and the remote ESS. Because the copy function occurs at the storage subsystem level, the application does no need to know of its existence. PPRC guarantees that the secondary copy is up-to-date by ensuring that the primary volume update will be successfully completed only when the primary ESS receives acknowledgement that the secondary copy has been successfully updated.

The sequence when updating records is as follows (refer to Figure 6-2):