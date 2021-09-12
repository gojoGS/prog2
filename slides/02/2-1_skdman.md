---
title: "Lesson 02.1: sdkman"
patat:
    incrementalLists: true
---

# Gyakran használt parancsok

- `sdk list`: artifactok listázása
- `sdk list java`: telepíthető JDK-k listázása
- `sdk install java 16.0.2.7.1-amzn`: 16.0.2.7.1-amzn verziójú JDK telepítése
- `sdk uninstall java 16.0.2.7.1-amzn`: 16.0.2.7.1-amzn verziójú JDK törlése
- `sdk use java 16.0.2.7.1-amzn`: 16.0.2.7.1-amzn verziójú JDK használata a jelenlegi shell sessionben
- `sdk default java 16.0.2.7.1-amzn`: 16.0.2.7.1-amzn verziójú JDK használata rendszer szinten

---

```bash
#THIS MUST BE AT THE END OF THE FILE FOR SDKMAN TO WORK!!!
export SDKMAN_DIR="/home/gojo/.sdkman"
[[ -s "/home/gojo/.sdkman/bin/sdkman-init.sh" ]] && source "/home/gojo/.sdkman/bin/sdkman-init.sh"
```
  