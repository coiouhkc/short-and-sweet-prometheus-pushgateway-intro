From the project repo root:

```
LOC=$(scc -i java --ci -f json | jq '.[0].Code')

cat <<EOF | curl --data-binary @- "http://localhost:9091/metrics/job/transition"
# TYPE loc counter
loc{repo="core-apps"} ${LOC}
EOF
```