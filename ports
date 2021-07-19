#!/usr/bin/env bash

netstat_output=$(sudo netstat -tulpn)

while IFS= read -r line; do
  if echo "$line" | grep -qE "[0-9]+"
  then
    ip_port=$(echo "$line" | awk '{print $4;}')
    pid=$(echo "$line" | awk '{print $7;}' | grep -Eo "[0-9]+")
    if [[ -n "$pid" && "$pid" -ne "1" ]]
    then
      command=$(ps -p "$pid" -o command | grep -v "COMMAND")
      echo "$ip_port -> $pid -> $command"
      echo ""
    fi
  fi
done <<< "$netstat_output"
