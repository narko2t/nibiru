#!/bin/bash

while :
do
password=<you paswrd>
valoper_address=<you valoper>
wallet_name=<you wallet>
address=<you address>
	echo $password | nibid tx distribution withdraw-rewards $valoper_address --from $wallet_name --commission --fees 5000unibi -y

	sleep 20s

	Available=$(nibid query bank balances $address --output json | jq -r '.balances | map(select(.denom == "unibi")) | .[].amount' | tr -cd [:digit:])
	Fees=10000
	Amount=$(($Available - $Fees))
	Amount_final=$Amount"unibi"


	echo $password | nibid tx staking delegate $valoper_address $Amount_final --from $wallet_name --fees 5000unibi -y
	date
	sleep 900s
done;
