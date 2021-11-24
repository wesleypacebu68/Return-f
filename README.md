# Return-f
#include &lt;MsgBoxConstants.au3> #include &lt;WinAPI.au3>  $hGUI = GUICreate("Test", 500, 500)  $cInput_1 = GUICtrlCreateInput("", 10, 10, 200, 20) $cInput_2 = GUICtrlCreateInput("", 10, 50, 200, 20) $cInput_3 = GUICtrlCreateInput("", 10, 90, 200, 20)  $cButton_1 = GUICtrlCreateButton("Button 1", 250, 10, 80, 30) $cButton_2 = GUICtrlCreateButton("Button 2", 250, 50, 80, 30) $cButton_3 = GUICtrlCreateButton("Button 3", 250, 90, 80, 30)  $cEnter = GUICtrlCreateDummy()  GUISetState()  Local $aAccelKeys[2][2] = [["{ENTER}", $cEnter], ["{TAB}", $cEnter]] ; Make {TAB} an accelerator GUISetAccelerators($aAccelKeys)  While 1      Switch GUIGetMsg()         Case $GUI_EVENT_CLOSE             Exit         Case $cEnter             Switch  _WinAPI_GetFocus()                 Case GUICtrlGetHandle($cInput_1)                     ; Check the input content                     If checkEntry() = True Then                         ; Correct so move to next input                         GUICtrlSetState($cInput_2, $GUI_FOCUS)                     EndIf                     ; Not correct so stay in current input                 Case GUICtrlGetHandle($cInput_2)                     If checkEntry() = True Then                         GUICtrlSetState($cInput_3, $GUI_FOCUS)                     EndIf                 Case GUICtrlGetHandle($cInput_3)                     If checkEntry() = True Then                         ConsoleWrite("End" &amp; @CRLF)                     EndIf                 Case Else                     GUISetAccelerators(0)                     ; Remove accelerator link                     ControlSend($hGUI, "", "", "{TAB}")       ; Send {TAB} to the GUI                     GUISetAccelerators($aAccelKeys)           ; Reset the accelerator              EndSwitch     EndSwitch  WEnd  Func checkEntry()      ; Random chance of correct answer or fail     If Mod(@SEC, 2) = 0 Then         MsgBox($MB_SYSTEMMODAL, "Test Fail", "Press Enter to close this message box" )         Return False     EndIf     Return True  EndFunc
