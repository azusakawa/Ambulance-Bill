# Ambulance-Bill

* esx_ambulancejob\client\job.lua code 
## Bill
```
{label = _U('billing'),   value = 'billing'},
```

## Function
```
if data.current.value == 'billing' then
	ESX.UI.Menu.Open('dialog', GetCurrentResourceName(), 'billing', {
		title = _U('invoice_amount')
	}, function(data, menu)
			
	local amount = tonumber(data.value)
	if amount == nil then
		ESX.ShowNotification(_U('amount_invalid'))
	else
		menu.close()
		local closestPlayer, closestDistance = ESX.Game.GetClosestPlayer()
        if closestPlayer == -1 or closestDistance > 3.0 then
			ESX.ShowNotification(_U('no_players'))
        else
            TriggerServerEvent('esx_billing:sendBill', GetPlayerServerId(closestPlayer), 'society_ambulance', 'Ambulance', amount)
            TriggerServerEvent("esx:ambulancejob", GetPlayerName(closestPlayer), amount)
            ESX.ShowNotification(_U('billing_sent'))
        end
    end		
end, function(data, menu)
  menu.close()
end)
```

===============================================================================
* esx_ambulancejob\locales\en.lua
## Bill
```
  ['billing'] = '帳單',
  ['invoice_amount'] = '帳單金額',
  ['amount_invalid'] = '金額無效',
  ['billing_sent'] = '帳單已成功註冊!',
```
