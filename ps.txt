
$path=Read-Host 'what is the path to serials1.txt?'
$serials=Get-Content -Path $path -TotalCount 20
$dellurl="www.dell.com/support/home/us/en/19/product-support/servicetag/"
$serials.length
foreach ($serial in $serials) {
$fullurl= $dellurl + $serial + "/warranty?ref=captchasuccess"
$IE=new-object -com internetexplorer.application
$IE.navigate2($fullurl)
$IE.visible=$true
sleep 5
}