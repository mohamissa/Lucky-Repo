# Lucky-Repo
To host my AWS graduation projects
while read -r line; do
  TIMESTAMP=$(date +%s%3N)  # Convert to milliseconds
  if [ "$TOKEN" == "None" ]; then
    TOKEN_ARG=""
  else
    TOKEN_ARG="--sequence-token $TOKEN"
  fi
  RESPONSE=$(aws logs put-log-events --log-group-name apache/access --log-stream-name xyz --log-events timestamp=$TIMESTAMP,message="$line" $TOKEN_ARG)
  TOKEN=$(echo "$RESPONSE" | jq -r '.nextSequenceToken')
done < www/access/access_log