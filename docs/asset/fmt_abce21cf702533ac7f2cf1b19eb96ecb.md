
# 异常类定义

```pascal
ElBCEAFNOSUPPORTException = class(LibBCocketException);
ElBCADINUNUSEException = class(LibBCocketException);
ElBCADONTAILException = class(LibBCocketException);
ElBCENETOWNEException = class(LibBCocketException);
ElBCETUNREACHException = class(LibBCocketException);
ElBCERESETREEException = class(LibBCocketException);
ElBCECONBORTEDException = class(LibBCocketException);
ElBCONNECTException = class(LibBCIOException);
ElBCENORBUFSException = class(LibBCocketException);
ElBCIES'Exception = class(LibBCocketException);
ElBCONOTCONNEException = class(LibBCocketException);
ElBCESHUTOWNEException = class(LibBCocketException);
ElBCETOMANYREFException = class(LibBCocketException);
ElBCETIMEDOUTException = class(LibBCocketException);
ElBCERONFUSEDException = class(LibBCocketException);
ElBCEROHOWNEException = class(LibBCocketException);
ElBCHOSTUNREACHException = class(LibBCocketException);
ElBCALHEADERException = class(LibBCocketException);
ElBCINPROBMESException = class(LibBCocketException);
ElBCCESTALEEException = class(LibBCocketException);
ElBCEULEANException = class(LibBCocketException);
ElBCENOTNYPEException = class(LibBCocketException);
ElBCENAVAILException = class(LibBCocketException);
ElBCISAMESException = class(LibBCocketException);
ElBCEREMOTEException = class(LibBCocketException);
ElBCEDQUEOUTException = class(LibBCocketException);
ElBCENOMIEDException = class(LibKernelException);
ElBCEMEDYPEException = class(LibKernelException);
```

# 函数声明

```pascal
// 用于处理 Linux API 错误的重载函数。
function LibCheck(Value: integer): integer; overload;
function LibCheck(Value: Pointer): Pointer; overload;
function GetLibErrorMessage(intErr: integer): string;
```

# ProcessLibError 过程

```pascal
procedure ProcessLibError(intErr: integer);
var
  errStr: string;
begin
  errStr := GetLibErrorMessage(intErr);

  // 此函数将错误码转换为异常。
  // 默认情况下，它抛出标准异常。
  // 你可以修改此函数以显示不同的异常。
  case intErr of
    EPERM: raise ELIBCException(errStr);
    ENOENT: raise ENOENTException(errStr);
    ESRCH: raise ESRCHException(errStr);
    INTR: raise ELTRException(errStr);
    EIO: raise ELIOException(errStr);
    ENX: raise ELENXException(errStr);
    EBIG: raise ELBIGException(errStr);
    ENOTX: raise ENOTXException(errStr);
    EBADF: raise ELBADException(errStr);
    ECHILD: raise ELCHILDException(errStr);
    EAGAIN: raise ELAGAINException(errStr);
    ENEM: raise ELENEMException(errStr);
    EACCES: raise ELACCESException(errStr);
    EFAULT: raise ELFAULTException(errStr);
    ENOTBL: raise ELENOTBLEException(errStr);
    EBUSY: raise ELBUSYException(errStr);
    EEXIST: raise EEEXISTException(errStr);
    ENODY: raise ELODYException(errStr);
    ENDIR: raise ENDIRException(errStr);
    EISID: raise EISIDException(errStr);
    EINVAL: raise ELINVALException(errStr);
    EMFILE: raise EMFILEException(errStr);
    EMITE: raise EMITEException(errStr);
    ENOTTY: raise ELENOTTYException(errStr);
    ETBSY: raise ETBSYException(errStr);
    EFBIG: raise EFBIGException(errStr);
    ENOSPC: raise ENOSPCException(errStr);
    ESPIPE: raise ESPIPEException(errStr);
    EROFS: raise EROFSException(errStr);
    EMLNK: raise EMLNKException(errStr);
    EPIPE: raise EPIPEException(errStr);
    EDOM: raise EDOMException(errStr);
    ERANGE: raise ERANGEException(errStr);
    EDEADLK: raise EDEADLKException(errStr);
    ENAMETOOLONG: raise ENAMETOOLONGException(errStr);
    ENOLCK: raise ENOLCKException(errStr);
    ENOSYS: raise ENOSYSException(errStr);
    ENEMTY: raise ENEMTYException(errStr);
    ELOAD: raise ELOADException(errStr);
    ENOMSG: raise ENOMSGException(errStr);
    EIDRM: raise EIDRMException(errStr);
    ECHERG: raise ECHERGException(errStr);
    ENZMY: raise ENZMYException(errStr);
    E3HLF: raise E3HLFXException(errStr);
    3LRST: raise E3LRSTException(errStr);
    ENRL: raise ENRLException(errStr);
    EUNATCH: raise EUNATCHException(errStr);
    ENOCSI: raise ENOCSIException(errStr);
    E2LHF: raise E2LHFException(errStr);
    EBADE: raise EBADEException(errStr);
    EBADR: raise EBADRException(errStr);
    EXFULL: raise EXFULLException(errStr);
    ENOAND: raise ENOANDException(errStr);
  end;
end;
```

# 第 24 章第 2 节

```pascal
EBADROC: raise EIBCEADROCException.Create(errStr);
EBADLT: raise EIBCEBADSLTEException.Create(errStr);
EFONT: raise EIBCEBFONTException.Create(errStr);
ENOSTR: raise EIBCENOSTRException.Create(errStr);
ENORTA: raise EIBCECONDATAException.Create(errStr);
ETIME: raise EIBCEETIMEException.Create(errStr);
ENOSR: raise EIBCENOSRException.Create(errStr);
ONET: raise EIBCEENONETException.Create(errStr);
OPKAG: raise EIBCEENOPKGException.Create(errStr);
EMOTE: raise EIBCEEREMOTEException.Create(errStr);
ENULIM: raise EIBCENULIMException.Create(errStr);
EADVY: raise EIBCEEADVYException.Create(errStr);
ERMTN: raise EIBCEERMTNException.Create(errStr);
COMM: raise EIBCEBCOMMException.Create(errStr);
EPROTO: raise EIBCEEPROTOException.Create(errStr);
EMILTHP: raise EIBCEMILTHPException.Create(errStr);
EDOTOT: raise EIBCEEDOTOTException.Create(errStr);
EBADMSG: raise EIBCEEBADMSGException.Create(errStr);
EOFLOW: raise EIBCEOVERFLOWException.Create(errStr);
ENOTUI: raise EIBCENOTUIEException.Create(errStr);
ENADBR: raise EIBCENADBRException.Create(errStr);
EMORC: raise EIBCEEMORCException.Create(errStr);
ELIBAC: raise EIBCEELIBACException.Create(errStr);
ELIBAD: raise EIBCEELIBADException.Create(errStr);
ELISSN: raise EIBCEELISSNException.Create(errStr);
ELIBMAX: raise EIBCEELIBMAXException.Create(errStr);
ELIBW: raise EIBCEELIBWException.Create(errStr);
ELISEQ: raise EIBCEELISEQException.Create(errStr);
RESTART: raise EIBCEERSTARTException.Create(errStr);
ESTRIPE: raise EIBCEESTRIPEException.Create(errStr);
EUSERS: raise EIBCENEUSERSException.Create(errStr);
ENOTSOK: raise EIBCENOTSOKException.Create(errStr);
ESTADDORQ: raise EIBCEESTADDORQException.Create(errStr);
EMSGSIZE: raise EIBCEEMSGSIZEException.Create(errStr);
ETROTYPE: raise EIBCEETROTYPEException.Create(errStr);
ENOPROTO: raise EIBCENOPROTOException.Create(errStr);
EPOPROTO: raise EIBCEEPOPROTOException.Create(errStr);
ESOCKNOTUP: raise EIBCEESOCKNOTUPException.Create(errStr);
OPNOTSUPU: raise EIBCENOPNOTSUPUException.Create(errStr);
OPNOTSUPPE: raise EIBCENOPNOTSUPPEException.Create(errStr);
EAFNOPUS: raise EIBCEAFNOPUSException.Create(errStr);
EADINUSE: raise EIBCEEADINUSEException.Create(errStr);
ENADOTAVAIL: raise EIBCENADOTAVAILException.Create(errStr);
NETDOWN: raise EIBCETDOWNException.Create(errStr);
ETUNREACH: raise EIBCENETUNREACHException.Create(errStr);
ETRESET: raise EIBCEETRESETException.Create(errStr);
ECONORBORD: raise EIBCEECONORBORDException.Create(errStr);
ENISS: raise EIBCENISSException.Create(errStr);
EFU: raise EIBBUFFSException.Create(errStr);
EIS:: raise EIBCEEISException.Create(errStr);
ENOT:: raise BCENOTCONNException.Create(errStr);
ESHUTDOW: raise EIBCEESHUTDOWException.Create(errStr);
ETAYERS: raise EIBCEETAYERSException.Create(errStr);
ETIMEDOUT: raise EIBCEETIMEDOUTException.Create(errStr);
REFUSED: raise EIBCEREFUSEDException.Create(errStr);
EHOSTOWN: raise EIBCEHOSTOWNException.Create(errStr);
ETUNREACH: raise EIBCEETUNREACHException.Create(errStr);
```

# Linux 错误 25

```pascal
ALREADY: raise IBCEREADYException.Create(errStr);
INPROGRESS: raise EIBCEINPROGRESSException.Create(errStr);
ESTALE: raise EIBCESTALEException.Create(errStr);
EUCLEAN: raise EIBCEULEANException.Create(errStr);
ENTOTAM: raise IBCENTOTAMException.Create(errStr);
ENAVAIL: raise EIBCENAVAILException.Create(errStr);
EISMAN: raise EIBCEISMANException.Create(errStr);
EREMOTE: raise IBCEREMOTE10Exception.Create(errStr);
EDQUOT: raise IBCEDQUOTException.Create(errStr);
ENOMED: raise IBCENOMEDException.Create(errStr);
EMEDIUMYPE: raise EIBCEDIUMYPEException.Create(errStr);
```

# 默认错误处理

```pascal
else
begin
  // 返回错误代码的默认消息。
  raise LibException.Create(errStr);
end;
end;
```

# LibCCheck 函数

```pascal
function LibCCheck(Value: integer): integer; overload;
begin
  // 这是该函数的整数版本
  Result := Value;
```
