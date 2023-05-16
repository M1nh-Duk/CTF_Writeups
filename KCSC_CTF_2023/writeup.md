# KCSC CTF 2023

<h1>
    Forensic Challenges 
</h1>

- Tin học văn phòng
- Dropper (hoàn thành sau cuộc thi)


<h2>
    Tin học văn phòng 
</h2>

![](https://hackmd.io/_uploads/SkWCtFkBh.png)

- Đề bài yêu cầu chúng ta phân tích 1 mẫu mã độc được ẩn giấu trong file docm(file chứa macro). 
- Do có chứa macro nên chúng ta thử dump macro đó ra thì thu được phần đầu của flag (Cần phải tìm tiếp giá trị trong biến <code>$phlac</code>)

![](https://hackmd.io/_uploads/ByjvY5JS2.png)

- Do không biết phân tích tĩnh nên mình sẽ sử dụng phương pháp phân tích động:)).
- Đầu tiên mở file và enable macro trong 1 môi trường an toàn 

![](https://hackmd.io/_uploads/H1ctJ51Sn.png)

- Có thể thấy được rằng mã độc này sẽ mã hóa các file quan trọng của chúng ta nên khá nguy hiểm. Tuy nhiên tác giả đã bỏ đi phần mã hóa đó. 

- Trong khi thực thi thì quan sát được rằng ngoài thông báo được hiện lên thì có thêm 1 cửa sổ Powershell hiện lên màn hình(là process con của WINWORD.EXE nên chắc chắn macro trong file docm này thực thi code Powershell).

![](https://hackmd.io/_uploads/H1vpycyS2.png)


- Vậy thì giờ đơn giản là đi kiếm payload của Powershell trong Powershell log thôi 

![](https://hackmd.io/_uploads/SkOCy9Jr3.png)

- Payload
```
JAB7AHAANAB5AEwAMAA0AEQAfQA9ACgAJwBNANkeJwArACcAdAAgACcAKwAnAHMAJwArACcA0R4gACcAKwAnAHQA4AAnACsAJwBpACAAJwArACcAbAAnACsAKAAiAHsAMQB9AHsAMAB9ACIAIAAtAGYAIAAnAHUAIAAnACwAJwBpAMceJwApACsAJwBxAHUAYQAnACsAJwBuACAAJwArACcAdAByAM0eJwArACcAbgBnACAAJwArACcAYwDnHmEAJwArACcAIAAnACsAJwBiACcAKwAnAKEebgAgACcAKwAnABEBJwArACcA4wAgACcAKwAnAGIAyx4nACsAJwAgACcAKwAnAG0AJwArACcA4wAgACcAKwAoACgAIgBoAPMAYQAhACEAYABuABABwx4gACIAKwAnACcAKQArACcAJwApACsAKAAiAHsAMAB9AHsAMQB9ACIAIAAtAGYAIAAnABEBsAEnACwAJwDjHmMAJwApACsAJwAgACcAKwAnAGgAsAHbHicAKwAnAG4AZwAgACcAKwAnAGQAJwArACcAqx5uACAAJwArACcAZwBpAKMeJwArACcAaQAgACcAKwAnAG0AJwArACcA4wAsACAAJwArACcAYgChHm4AJwArACcAIAAnACsAJwBjAKceJwArACcAbgAgACcAKwAoACIAewAxAH0AewAwAH0AIgAgAC0AZgAnAHUAeQAnACwAJwBjAGgAJwApACsAJwDDHicAKwAnAG4AIAAnACsAJwBrAGgAJwArACgAIgB7ADEAfQB7ADAAfQAiAC0AZgAnAKMebgAgACcALAAnAG8AJwApACsAJwAxACcAKwAoACIAewAwAH0AewAxAH0AIgAtAGYAIAAnADAAMAAnACwAJwBrACAAJwApACsAJwB2AOAAJwArACcAbwAgACcAKwAnAHMAJwArACcA0R4gACcAKwAnAHQA4ABpACcAKwAnACAAJwArACgAIgB7ADEAfQB7ADAAfQAiACAALQBmACcAox4nACwAJwBrAGgAbwAnACkAKwAnAG4AJwArACcAIAAnACsAKAAoACIAcwBhAHUAOgBgAG4AMQAwADEAMAAxADAANwAxADEAMgAwADAAMABgAG4AQwBoAOceIAAiACsAJwAnACkAKwAnACcAKQArACcAdADgACcAKwAnAGkAIAAnACsAJwBrAGgAJwArACgAIgB7ADEAfQB7ADAAfQAiACAALQBmACAAJwA6ACcALAAnAG8Aox5uACcAKQArACcAIAAnACsAJwBOACcAKwAnAGcAdQB5ACcAKwAnAMUebgAgACcAKwAnAFQAaAAnACsAKAAiAHsAMQB9AHsAMAB9ACIAIAAtAGYAJwAgACcALAAnAGEAbgBoACcAKQArACgAKAAiAEwAbwBuAGcAYABuAE4AZwDiAG4AIAAiACsAJwAnACkAKwAnACcAKQArACcAaAAnACsAKAAiAHsAMAB9AHsAMQB9ACIAIAAtAGYAIAAnAOAAbgBnACcALAAnACAAJwApACsAJwBNACcAKwAnAEIAIAAnACsAJwBCAGEAJwArACcAbgBrACcAKQANAAoAJgAoACcAQQAnACsAJwBkACcAKwAoACIAewAwAH0AewAxAH0AIgAtAGYAIAAnAGQALQBUACcALAAnAHkAcABlACcAKQApACAALQBBAHMAcwBlAG0AYgBsAHkATgBhAG0AZQAgACgAIgB7ADEAfQB7ADYAfQB7ADAAfQB7ADMAfQB7ADUAfQB7ADQAfQB7ADIAfQAiAC0AZgAgACcAdAAuAFYAJwAsACgAIgB7ADAAfQB7ADEAfQAiAC0AZgAgACcATQBpAGMAcgAnACwAJwBvAHMAJwApACwAJwBpAGMAJwAsACcAaQBzACcALAAoACIAewAxAH0AewAwAH0AIgAgAC0AZgAgACcAcwAnACwAJwBsAEIAYQAnACkALAAnAHUAYQAnACwAJwBvAGYAJwApADsADQAKAHMAZQBUAC0ASQB0AEUATQAgACgAIgBWACIAKwAiAGEAcgBJAGEAYgAiACsAIgBsAGUAOgBoAFYASQA5ADYAIgApACAAKAAgAFsAVAB5AHAARQBdACgAIgB7ADQAfQB7ADUAfQB7ADcAfQB7ADEAfQB7ADMAfQB7ADYAfQB7ADAAfQB7ADgAfQB7ADIAfQAiACAALQBGACAAJwBjAC4ASQBuAFQARQBSACcALAAnAGIAJwAsACcASQBPAE4AJwAsACcAYQAnACwAJwBtAGkAQwByAE8AcwBPAGYAJwAsACcAdAAuAFYAaQBTACcALAAnAHMASQAnACwAJwB1AEEAbAAnACwAJwBBAEMAVAAnACkAIAApACAAOwAgAFMARQB0AC0AaQB0AEUATQAgACgAJwB2AEEAJwArACcAUgBpAGEAYgAnACsAJwBsAGUAOgAnACsAJwBPADcAdgAnACsAJwA4AGsAJwApACAAIAAoACAAIABbAFQAWQBQAEUAXQAoACIAewA0AH0AewA1AH0AewAzAH0AewAyAH0AewAwAH0AewAxAH0AIgAtAEYAIAAnAC4ATQBTAEcAQgBPAHgAUwB0ACcALAAnAHkATABlACcALAAnAC4AVgBJAHMAdQBhAGwAYgBBAFMAaQBjACcALAAnAFMAbwBmAHQAJwAsACcATQBpAEMAJwAsACcAcgBPACcAKQAgACAAKQAgADsAIAAgACAAIAAoACAAZwBlAHQALQB2AEEAUgBJAEEAQgBsAEUAIAAoACcAaAB2AEkAOQAnACsAJwA2ACcAKQAgACAALQB2AGEAbABVAEUATwBOAGwAIAApADoAOgBNAHMAZwBCAG8AeAAoACQAewBwADQAeQBMADAANABEAH0ALAAgACAAJABPADcAVgA4AEsAOgA6AEkAbgBmAG8AcgBtAGEAdABpAG8AbgAsACAAKAAiAHsAMQB9AHsANAB9AHsAOAB9AHsAMQAxAH0AewA5AH0AewAwAH0AewAyAH0AewAzAH0AewA2AH0AewAxADAAfQB7ADcAfQB7ADUAfQAiACAALQBmACAAJwBjAPkAbgBnACAAdABoALABoQFuAGcAJwAsACcAQwBoAPoAJwAsACcAIAAnACwAJwB0ACcALAAnAG4AZwAgAHQA9AAnACwAJwBpAG4AJwAsACcAaQAnACwAJwAgAHQAJwAsACcAaQAgACcALAAnACAAJwAsACcAvx5jACAAYgDhAG8AJwAsACcAIAB2APQAJwApACkAOwANAAoALgAoACIAewAzAH0AewAwAH0AewAxAH0AewAyAH0AIgAgAC0AZgAoACIAewAxAH0AewAwAH0AIgAtAGYAIAAnAHQAcAAnACwAJwAtAE8AdQAnACkALAAnAHUAJwAsACcAdAAnACwAKAAiAHsAMAB9AHsAMQB9ACIALQBmACcAVwAnACwAJwByAGkAdABlACcAKQApACAAJAB7AHAANAB5AEwAMAA0AEQAfQAgAHwAIAAuACgAIgB7ADEAfQB7ADAAfQB7ADIAfQAiACAALQBmACgAIgB7ADAAfQB7ADEAfQB7ADIAfQAiAC0AZgAnAHUAJwAsACcAdAAtACcALAAnAEYAaQBsACcAKQAsACcATwAnACwAJwBlACcAKQAgAC0ARQBuAGMAbwBkAGkAbgBnACAAKAAiAHsAMQB9AHsAMAB9ACIALQBmACcAZgA4ACcALAAnAHUAdAAnACkAIAAiAEMAOgBcAFUAcwBlAHIAcwBcACQAZQBuAHYAOgBVAHMAZQByAE4AYQBtAGUAXABEAGUAcwBrAHQAbwBwAFwASABhAGMAawBlAGQALgB0AHgAdAAiAA0ACgAkAHsAVwBzAGAAQwByAGkAcABUAH0AIAA9ACAALgAoACIAewAwAH0AewAyAH0AewAxAH0AIgAtAGYAJwBOAGUAdwAtAE8AJwAsACcAYwB0ACcALAAnAGIAagBlACcAKQAgAC0AYwBvAG0AIAAoACIAewAxAH0AewAwAH0AewAyAH0AIgAtAGYAJwBjACcALAAnAHcAcwAnACwAJwByAGkAcAB0AC4AcwBoAGUAbABsACcAKQA7ACAAMQAuAC4ANQAwACAAfAAgAC4AKAAnACUAJwApACAAewAgACQAewB3AGAAUwBDAHIAaQBgAFAAdAB9AC4AIgBzAGAAZQBuAGQASwBgAEUAWQBzACIAKABbAGMAaABhAHIAXQAxADcANQApACAAfQA7AA0ACgAmACgAIgB7ADIAfQB7ADAAfQB7ADEAfQAiACAALQBmACAAJwB0ACcALAAnAGEAcgB0AC0AUAByAG8AYwBlAHMAcwAnACwAJwBTACcAKQAgACgAIgB7ADIAfQB7ADEAfQB7ADAAfQAiACAALQBmACAAJwBsAG8AcgBlACcALAAnAHAAJwAsACcAaQBlAHgAJwApACAALQBBAHIAZwB1AG0AZQBuAHQATABpAHMAdAAgACgAIgB7ADEAfQB7ADYAfQB7ADIAfQB7ADAAfQB7ADUAfQB7ADMAfQB7ADcAfQB7ADQAfQAiAC0AZgAgACcAdwB3AC4AeQBvAHUAdAB1AGIAZQAuAGMAJwAsACcALQBrACAAJwAsACcAOgAvAC8AdwAnACwAJwBtAC8AdwAnACwAJwBwAFIAcQBzADQAawAnACwAJwBvACcALAAnAGgAdAB0AHAAcwAnACwAJwBhAHQAYwBoAD8AdgA9AEIATQBFAGQAQgAnACkADQAKACQAewBwAGgAbABhAGMAfQA9ACgAIgB7ADIAfQB7ADUAfQB7ADAAfQB7ADQAfQB7ADEAfQB7ADMAfQAiACAALQBmACAAJwB5ACcALAAoACIAewAyAH0AewAxAH0AewAwAH0AIgAgAC0AZgAgACgAIgB7ADIAfQB7ADEAfQB7ADAAfQAiACAALQBmACcASAAnACwAKAAiAHsAMAB9AHsAMQB9ACIAIAAtAGYAJwBfAGEAJwAsACcAaAAxACcAKQAsACcAXwBtADMAJwApACwAJwAwAHQAJwAsACcAdQBfAGcAJwApACwAKAAiAHsAMAB9AHsAMgB9AHsAMQB9ACIALQBmACAAJwBUAHIAMAAnACwAKAAiAHsAMAB9AHsAMQB9ACIAIAAtAGYAIAAnADQAJwAsACgAIgB7ADAAfQB7ADEAfQAiACAALQBmACgAIgB7ADAAfQB7ADEAfQAiAC0AZgAnAGwAdwAnACwAJwBAAHIAJwApACwAJwAzACcAKQApACwAKAAiAHsAMQB9AHsAMAB9ACIALQBmACcAXwBtACcALAAnAGwAbAAnACkAKQAsACcAaQAnACwAJwAwACcALAAnAF8AJwApADsALgAoACIAewA0AH0AewAwAH0AewAzAH0AewAyAH0AewAxAH0AIgAtAGYAJwAtAFYAYQAnACwAJwBlACcALAAnAGEAYgBsACcALAAnAHIAaQAnACwAKAAiAHsAMAB9AHsAMQB9ACIAIAAtAGYAJwBSACcALAAoACIAewAwAH0AewAxAH0AIgAtAGYAJwBlAG0AbwAnACwAJwB2AGUAJwApACkAKQAgACgAIgB7ADEAfQB7ADAAfQAiACAALQBmACAAJwBjACcALAAoACIAewAwAH0AewAxAH0AIgAgAC0AZgAnAHAAaABsACcALAAnAGEAJwApACkA
```

- Có được payload (có vẻ là base64) rồi thì chúng ta có thể dùng CyberChef để decode hoặc sử dụng 1 tool có thể decode và deobfuscate luôn cho tiện. Đó là [https://github.com/R3MRUM/PSDecode](https://) 
- Chạy tool thì thu được đoạn script cuối cùng và có được giá trị của biến cần tìm và ghép được flag:
![](https://hackmd.io/_uploads/HkuFj5JB2.png)
<br>
<h2>
    Dropper
</h2>

![](https://hackmd.io/_uploads/Hkfz1ikHn.png)

- Bài không có description và chỉ cho chúng ta file <code>.vhdx</code>
- Đây cũng là 1 loại disk image nên có thể mount bằng FTK Imager

![](https://hackmd.io/_uploads/HyZuloJrn.png)

- Do "linh cảm" nên mình thử dump log của Powershell ra xem thử có vấn đề gì không và câu trả lời là có

![](https://hackmd.io/_uploads/ryvVfi1S2.png)

- Từng cái log warning cho thấy Powershell chạy 1 đoạn payload nào đó và chúng khác nhau. Vậy thì nhiệm vụ được đặt ra là đi tìm cái script mà gen ra cái payload đó.
- Sau khi tìm kiếm thì mình phát hiện được 1 file <code>readme.txt</code> khả nghi ở đường dẫn <code>C:\Users\Public\ChromeUpdate </code>

![](https://hackmd.io/_uploads/HkhNXsJrn.png)
 
 
- Tại sao trong 1 file txt lại hiển thị 1 cái script Powershell. Đó là vì file script nằm trong Alternate Data Stream của file txt.
- Dump file txt đó rồi mở bằng WinRar và extract thì chúng ta có được file <code>twenty.ps1</code> gốc
```
$ucgag = New-Object "System.Security.Cryptography.AesManaged"
$mjjonwq = [System.Convert]::FromBase64String("eLErcjnTWMBXK7T1sJtt71Ho6f3XvQxXVTWcHTPwqMg=")
$dijp = [System.Convert]::FromBase64String("lL/lTTROsR5QWLNprdNN+Xpl0e+E8c1qahEFr3CpLMV6pFON1jPVyU70hUBR0jQRLnwWx4TTCNpZ72fTQIrH1FmQZlZh+kEB8vcfGclwS0WLw6Ad4KHJppho6o7A8XjW39QwHWJ/Lh5bfILJmHvl5OOP/Sb4lTg+VTpgLM3Sw+c/76LzYXgNGCBeUTn4iwpHUF7RNoEZFhnIOF7Ngrwb6/tPKxLEcb2TBT1Xteb+S6uYPkePwQzXB13RgVDMwcY9/kX1LOaj4xmx81OdUGL+NpM6L5A+MD5NUVcV8/t7pETh4UxuhL/Wy86f112v0uNYK4rAGZfV53glXJvIFlM28WGN24Sv5aDwHmPQMkK6CyiU3o5IpinDovRfbE6BLQcoc/MU5/ViFSA/14lmzhQciq72iC9+ 
...ZK9mThJPO+2WvuHv7A==")
$ucgag.BlockSize = 128
$ucgag.Mode = [System.Security.Cryptography.CipherMode]::CBC
$ucgag.Padding = [System.Security.Cryptography.PaddingMode]::ISO10126
$ucgag.KeySize = 128
$ucgag.Key = $mjjonwq
$ucgag.IV = $dijp[0..15]
$ojcibsmux = New-Object System.IO.MemoryStream
$sxgxkrpr = New-Object System.IO.MemoryStream(,$ucgag.CreateDecryptor().TransformFinalBlock($dijp,16,$dijp.Length-16))
$ymqwadtn = New-Object System.IO.Compression.GzipStream $sxgxkrpr, ([IO.Compression.CompressionMode]::Decompress)
$ymqwadtn.CopyTo($ojcibsmux)
$ymqwadtn.Close()
$kqszth = [System.Text.Encoding]::UTF8.GetString($ojcibsmux.ToArray())
Write-Output $kqszth
$sxgxkrpr.Close()
$ucgag.Dispose()
IEX($kqszth)
```
- Về cơ bản thì đoạn script này sẽ decode base64 đoạn string trong biến <code>$ucgag</code> rồi tiến hành decrypt nó bằng thuật toán cung cấp và cuối cùng là thực thi (IEX). 
- Vậy nên,thay vì thực thi câu lệnh được lưu trong biến <code>$kqszth </code> thì sửa thành in ra giá trị mà nó mang
![](https://hackmd.io/_uploads/H1aOPhJr3.png)
- Output đưa ra lại là 1 đoạn script mới với nội dung tương tự, tiếp tục lấy đoạn script này thực thi 

(Đến đây thì sau khoảng 10 lần thử chạy bằng cơm mình đã nghĩ đây chỉ là fake thôi nên bỏ hướng này và đi tìm manh mối khác nhưng cuối cùng sau giải kết thúc mình mới biết được rằng flag nằm ở đoạn script cuối cùng và từng đoạn script được tạo mới ra tương ứng với số log Warning ghi lại trong Powershell log)

- Cuối cùng sau khoảng 20 lần thì ta có được đoạn script final
```
$src1 = "/9j/4AAQSkZJRgABAQEAYABgAAD/4gHYSUNDX1BST0ZJTEUAAQEAAAHIbGNtcwIQAABtbnRyUkdCIFhZWiAH4gADABQACQAOAB1hY3NwTVNGVAAAAABzYXdzY3RybAAAAAAAAAAAAAAAAAAA9tYAAQA
 ...kzSUlAh4NBNMzTSfWgB5NN60tFABSUZooAUU7NNFOoASiloNACUlKeajJoGONFMooEf/Z"

$destpath = "C:\Users\Public\KaCeEtCe"
$dest1 = "C:\Users\Public\KaCeCEtCe\K"
$dest2 = "C:\Users\Public\KaCeCEtCe\C"
$dest3 = "C:\Users\Public\KaCeCEtCe\S"
$dest4 = "C:\Users\Public\KaCeCEtCe\C2"

$ComputerName = "KCSC-Jang","KCSC-Bquanman","KCSC-Ạomix","KCSC-LilThawg29","KCSC
    -DuongCuc"
if (!(Test-Path -Path $destpath)){
        New-Item -Path $destpath -ItemType Directory
}
foreach($x in $ComputerName){
    if($env:COMPUTERNAME -eq $x){
        $decodedCommand = [Convert]::FromBase64String($src1)
        [io.file]::WriteAllBytes($destpath,$decodedCommand)
        $decodedCommand = [Convert]::FromBase64String($src1)
        [io.file]::WriteAllBytes($destpath,$decodedCommand)
        $decodedCommand = [Convert]::FromBase64String($src1)
        [io.file]::WriteAllBytes($destpath,$decodedCommand)
        $decodedCommand = [Convert]::FromBase64String($src1)
        [io.file]::WriteAllBytes($destpath,$decodedCommand)
        }
    }
```
- Về cơ bản thì đoạn script này chỉ có tác dụng decode đoạn base64 và tạo ra 1 file mới với từng byte là giá trị của đoạn base64 vừa rồi. Sửa đổi 1 chút và chạy thì ta thu được ảnh jpg có chứa flag
  