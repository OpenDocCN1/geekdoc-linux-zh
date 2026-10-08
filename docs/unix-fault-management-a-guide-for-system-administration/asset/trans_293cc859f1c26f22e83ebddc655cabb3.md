
## 附录 A-3 续

- [4] nlHostOutPkts
- [5] nlHostInOctets
- [6] nlHostOutOctets
- [7] nlHostOutMacNonUnicastPkts
- [8] nlHostCreateTime
- [15] nlMatrix
  - [1] nlMatrixControlTable
    - [1] nlMatrixControlEntry
      - [1] nlMatrixControlIndex*
      - [2] nlMatrixControlDataSource
      - [3] nlMatrixControlNlDroppedFrames
      - [4] nlMatrixControlNlInserts
      - [5] nlMatrixControlNlDeletes
      - [6] nlMatrixControlNlMaxDesiredEntries
      - [7] nlMatrixControlAlDroppedFrames
      - [8] nlMatrixControlAlInserts
      - [9] nlMatrixControlAlDeletes
      - [10] nlMatrixControlAlMaxDesiredEntries
      - [11] nlMatrixControlOwner
      - [12] nlMatrixControlStatus
  - [2] nlMatrixSDTable
    - [1] nlMatrixSDEntry
      - [1] nlMatrixSDTimeMark*
      - [2] nlMatrixSDSourceAddress
      - [3] nlMatrixSDDestAddress
      - [4] nlMatrixSDPkts
      - [5] nlMatrixSDOctets
      - [6] nlMatrixSDCreateTime
  - [3] nlMatrixDSTable
    - [1] nlMatrixDSEntry
      - [1] nlMatrixDSTimeMark*
      - [2] nlMatrixDSSourceAddress
      - [3] nlMatrixDSDestAddress
      - [4] nlMatrixDSPkts
      - [5] nlMatrixDSOctets
      - [6] nlMatrixDSCreateTime
  - [4] nlMatrixTopNControlTable
    - [1] nlMatrixTopNControlEntry
      - [1] nlMatrixTopNControlIndex*
      - [2] nlMatrixTopNControlMatrixIndex
      - [3] nlMatrixTopNControlRateBase
      - [4] nlMatrixTopNControlTimeRemaining
      - [5] nlMatrixTopNControlGeneratedReports
      - [6] nlMatrixTopNControlDuration
      - [7] nlMatrixTopNControlRequestedSize
      - [8] nlMatrixTopNControlGrantedSize
      - [9] nlMatrixTopNControlStartTime
      - [10] nlMatrixTopNControlOwner
      - [11] nlMatrixTopNControlStatus
  - [5] nlMatrixTopNTable
    - [1] nlMatrixTopNEntry
      - [1] nlMatrixTopNIndex*
      - [2] nlMatrixTopNProtocolDirLocalIndex
      - [3] nlMatrixTopNSourceAddress
      - [4] nlMatrixTopNDestAddress
      - [5] nlMatrixTopNPktRate
      - [6] nlMatrixTopNReversePktRate
      - [7] nlMatrixTopNOctetRate
      - [8] nlMatrixTopNReverseOctetRate
- [16] alHost
  - [1] alHostTable
    - [1] alHostEntry
      - [1] alHostTimeMark*
      - [2] alHostInPkts
      - [3] alHostOutPkts
      - [4] alHostInOctets
      - [5] alHostOutOctets
      - [6] alHostCreateTime
- [17] alMatrix
  - [1] alMatrixSDTable
    - [1] alMatrixSDEntry
      - [1] alMatrixSDTimeMark*
      - [2] alMatrixSDPkts
      - [3] alMatrixSDOctets
      - [4] alMatrixSDCreateTime
  - [2] alMatrixDSTable
    - [1] alMatrixDSEntry
      - [1] alMatrixDSTimeMark*
      - [2] alMatrixDSPkts
      - [3] alMatrixDSOctets
      - [4] alMatrixDSCreateTime
  - [3] alMatrixTopNControlTable
    - [1] alMatrixTopNControlEntry
      - [1] alMatrixTopNControlIndex*
      - [2] alMatrixTopNControlMatrixIndex
      - [3] alMatrixTopNControlRateBase
      - [4] alMatrixTopNControlTimeRemaining
      - [5] alMatrixTopNControlGeneratedReports
      - [6] alMatrixTopNControlDuration
      - [7] alMatrixTopNControlRequestedSize
      - [8] alMatrixTopNControlGrantedSize
      - [9] alMatrixTopNControlStartTime
      - [10] alMatrixTopNControlOwner
      - [11] alMatrixTopNControlStatus
  - [4] alMatrixTopNTable
    - [1] alMatrixTopNEntry
      - [1] alMatrixTopNIndex*
      - [2] alMatrixTopNProtocolDirLocalIndex
      - [3] alMatrixTopNSourceAddress
      - [4] alMatrixTopNDestAddress
      - [5] alMatrixTopNAppProtocolDirLocalIndex
      - [6] alMatrixTopNPktRate
      - [7] alMatrixTopNReversePktRate
      - [8] alMatrixTopNOctetRate
      - [9] alMatrixTopNReverseOctetRate
- [18] usrHistory
  - [1] usrHistoryControlTable
    - [1] usrHistoryControlEntry
      - [1] usrHistoryControlIndex*
      - [2] usrHistoryControlObjects
      - [3] usrHistoryControlBucketsRequested
      - [4] usrHistoryControlBucketsGranted
      - [5] usrHistoryControlInterval
      - [6] usrHistoryControlOwner
      - [7] usrHistoryControlStatus
  - [2] usrHistoryObjectTable
    - [1] usrHistoryObjectEntry
      - [1] usrHistoryObjectIndex*
      - [2] usrHistoryObjectVariable
      - [3] usrHistoryObjectSampleType
      - [3] usrHistoryTable
    - [1] usrHistoryEntry
      - [1] usrHistorySampleIndex*
      - [2] usrHistoryIntervalStart
      - [3] usrHistoryIntervalEnd
      - [4] usrHistoryAbsValue
      - [5] usrHistoryValStatus
- [19] probeConfig
  - [1] probeCapabilities
  - [2] probeSoftwareRev
  - [3] probeHardwareRev
  - [4] probeDateTime
  - [5] probeResetControl
  - [6] probeDownloadFile
  - [7] probeDownloadTFTPServer
  - [8] probeDownloadAction
  - [9] probeDownloadStatus
  - [10] serialConfigTable
    - [1] serialConfigEntry
      - [1] serialMode
      - [2] serialProtocol
      - [3] serialTimeout
      - [4] serialModemInitString
      - [5] serialModemHangUpString
      - [6] serialModemConnectResp
      - [7] serialModemNoConnectResp
      - [8] serialDialoutTimeout
      - [9] serialStatus
  - [11] netConfigTable
    - [1] netConfigEntry
      - [1] netConfigIPAddress
      - [2] netConfigSubnetMask
      - [3] netConfigStatus
  - [12] netDefaultGateway
  - [13] trapDestTable
    - [1] trapDestEntry
      - [1] trapDestIndex*
      - [2] trapDestCommunity
      - [3] trapDestProtocol
      - [4] trapDestAddress
      - [5] trapDestOwner
      - [6] trapDestStatus
  - [14] serialConnectionTable
    - [1] serialConnectionEntry
      - [1] serialConnectIndex*
      - [2] serialConnectDestIpAddress
      - [3] serialConnectType
      - [4] serialConnectDialString
      - [5] serialConnectSwitchConnectSeq
      - [6] serialConnectSwitchDisconnectSeq
      - [7] serialConnectSwitchResetSeq
      - [8] serialConnectOwner
      - [9] serialConnectStatus
- [20] rmonConformance
  - [1] rmon2MIBCompliances
    - [1] rmon2MIBCompliance
    - [2] rmon2MIBApplicationLayerCompliance
  - [2] rmon2MIBGroups
    - [1] protocolDirectoryGroup
    - [2] protocolDistributionGroup
    - [3] addressMapGroup
    - [4] nlHostGroup
    - [5] nlMatrixGroup
    - [6] alHostGroup
    - [7] alMatrixGroup
    - [8] usrHistoryGroup
    - [9] probeInformationGroup
    - [10] probeConfigurationGroup
    - [11] rmon1EnhancementGroup
    - [12] rmon1EthernetEnhancementGroup
    - [13] rmon1TokenRingEnhancementGroup

### 监控说明

如果您打算编写自己的 SNMP 应用程序，RMON MIB 的数字根 OID 为 1.3.6.1.2.1.16。RMON II 是该 MIB 的扩展。

协议目录列出了监视器支持的所有协议。监视器可以添加更多协议，但扩展性有限。

协议分布组显示了局域网段上正在发送的数据量和数据包量的每协议统计数据。通过此信息，您可以计算每协议的带宽利用率，并有望隔离出存在问题的应用程序。

地址映射组用于将网络地址映射到其绑定的站点地址。网络层主机组随后显示每个网络地址的流量大小。网络层矩阵组显示网络地址对之间的网络流量统计数据。您还可以看到流量最大的前几名生成者。

应用层主机显示特定网络地址的网络流量统计数据，并按协议细分。类似地，应用层矩阵显示网络地址对之间流量的此类信息。

### 主机资源 MIB

主机资源 MIB 是一个用于表示主机信息的 IETF 建议标准。该 MIB 要求实现 MIB-II 的部分内容。主机资源 MIB 包含的信息包括系统当前的最大进程数和最大进程数，以及系统运行时间。此 MIB 可用于表示有关计算机系统或设备（如网络打印机）的信息。

#### MIB 定义

附录 A-4 展示了 RFC 1514 中定义的主机资源 MIB 的完整规范。

#### 附录 A-4 主机资源 MIB 规范。

- mib_2
  - [25] host
    - [1] hrSystem
      - [1] hrSystemUptime
      - [2] hrSystemDate
      - [3] hrSystemInitialLoadDevice
      - [4] hrSystemInitialLoadParameters
      - [5] hrSystemNumUsers
      - [6] hrSystemProcesses
      - [7] hrSystemMaxProcesses
    - [2] hrStorage
      - [1] hrStorageTypes
        - [1] hrStorageOther
        - [2] hrStorageRam
        - [3] hrStorageVirtualMemory
        - [4] hrStorageFixedDisk
        - [5] hrStorageRemovableDisk
        - [6] hrStorageFloppyDisk
        - [7] hrStorageCompactDisc
        - [8] hrStorageRamDisk
      - [2] hrMemorySize
      - [3] hrStorageTable
        - [1] hrStorageEntry
          - [1] hrStorageIndex*
          - [2] hrStorageType
          - [3] hrStorageDescr
          - [4] hrStorageAllocationUnits
          - [5] hrStorageSize
          - [6] hrStorageUsed
          - [7] hrStorageAllocationFailures
    - [3] hrDevice
      - [1] hrDeviceTypes
        - [1] hrDeviceOther
        - [2] hrDeviceUnknown
        - [3] hrDeviceProcessor
        - [4] hrDeviceNetwork
        - [5] hrDevicePrinter
        - [6] hrDeviceDiskStorage
        - [10] hrDeviceVideo
        - [11] hrDeviceAudio
        - [12] hrDeviceCoprocessor
        - [13] hrDeviceKeyboard
        - [14] hrDeviceModem
        - [15] hrDeviceParallelPort
        - [16] hrDevicePointing
        - [17] hrDeviceSerialPort
        - [18] hrDeviceTape
        - [19] hrDeviceClock

