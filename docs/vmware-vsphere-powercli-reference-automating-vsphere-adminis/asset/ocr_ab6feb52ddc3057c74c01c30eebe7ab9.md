```
{
  if ($Conf.Key.ToString()) -eq $VM.Id.ToString())\  {
    $Msg = "Setting $($VM.Name) start order to:"
    Switch ($PSCmdlet.MyInvocation.BoundParameters){
      'StartOrder'
      {
        $Msg = "{0} StartOrder:{1}" -f $Msg, $StartOrder
        $Conf.StartOrder = $StartOrder
      }
      'StartDelay'
      {
        $Msg = "{0} StartDelay:{1}" -f $Msg, $StartDelay
        $Conf.StartDelay = $StartDelay
      }
      'WaitingForGuest'
      {
        $Msg = "{0} WaitingForGuest:{1}" -f $Msg, $WaitingForGuest
        $Conf.WaitingForGuest = $WaitingForGuest
      }
      'StartAction'
      {
        $Msg = "{0} StartAction:{1}" -f $Msg, $StartAction
        $Conf.StartAction = $StartAction
      }
      'StopDelay'
      {
        $Msg = "{0} StopDelay:{1}" -f $Msg, $StopDelay
        $Conf.StopDelay = $StopDelay
      }
      'StopAction'
      {
        $Msg = "{0} StopAction:{1}" -f $Msg, $StopAction
        $Conf.StopAction = $StopAction
      }
      'DestroyWithParent'
      {
        $Msg = "{0} DestroyWithParent:{1}" -f $Msg,
```