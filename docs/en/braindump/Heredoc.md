# Examples

## Evaluates variables
```bash
cat << EOF > file.sh
echo "I am $(whoami)"
EOF
```

## Does not evaluate variables
```bash
cat << 'EOF' > file.sh
echo "I am $(whoami)"
EOF
```
