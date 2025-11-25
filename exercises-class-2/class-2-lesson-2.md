# Class 2: Lesson 2

This is the second lesson for Class 2.

## Advanced Topics

In this lesson, we'll cover networking and connectivity.

## Task 1: Network Configuration

```bash
# Check network interfaces
ip addr show

# Check network connections
netstat -tuln

# Test connectivity
ping -c 3 8.8.8.8
```

## Task 2: System Services

```bash
# Check system services
systemctl list-units --type=service | head -10

# Check service status
systemctl status ssh
```

## Summary

You've learned about networking and system services.

---

**Duration:** 15 minutes  
**Difficulty:** Intermediate

