---


# 📡 Ethernet CRC-32 / Frame Check Sequence (FCS) Lab

**A low-level simulation of Ethernet error detection using the CRC-32 algorithm (IEEE 802.3 standard)**

---

## 📌 Project Overview

This project simulates how real Network Interface Cards (NICs) perform error detection at the **Data Link Layer** using the **CRC-32** algorithm. 

It demonstrates the exact process used in Ethernet frames for generating and verifying the **Frame Check Sequence (FCS)**, providing deep insight into bit-level operations that occur inside hardware.

The goal is educational: to understand how CRC works internally, rather than just using high-level library functions.

---

## 🎯 Learning Objectives

By studying and running this project, you will learn:

- How CRC-32 is computed bit-by-bit
- Why Ethernet uses a **reflected polynomial** and LSB-first processing
- How real NIC hardware generates and validates FCS
- The structure of an Ethernet II frame
- Why CRC is excellent for burst and single-bit error detection
- The difference between software simulation and hardware implementation

---

## 🔢 Theoretical Background

### CRC-32 Polynomial (Ethernet)

- **Normal Form**: `0x04C11DB7`
- **Reflected Form** (used in implementation): `0xEDB88320`

Ethernet processes data **LSB-first** to match the behavior of hardware shift registers.

### Computation Principle

CRC treats the data as a large binary polynomial and computes:

> `(data << 32) mod generator_polynomial`

### Initialization & Finalization (Ethernet Standard)

- **Initial Value**: `0xFFFFFFFF`
- **Final XOR**: `0xFFFFFFFF`

This improves error detection properties and is the industry standard.

---

## 🧩 Ethernet Frame Structure (Simplified)

```text
+-------------------+-------------------+------------+-------------------+---------+
| Dest MAC (6)      | Src MAC (6)       | EtherType (2) | Payload (N)       | FCS (4) |
+-------------------+-------------------+---------------+-------------------+---------+
```

- **Minimum frame size** (without FCS): 14 bytes
- **Minimum frame size** (with FCS): 18 bytes

---

## ⚙️ Core Features

### 1. CRC-32 Engine
- Pure bitwise implementation (no lookup table)
- Uses reflected polynomial `0xEDB88320`
- Matches real Ethernet hardware behavior

### 2. Frame Generation (`generate_frame`)
- Takes raw frame (without FCS)
- Computes CRC-32
- Appends FCS in **little-endian** byte order

### 3. Frame Verification (`verify_frame`)
- Extracts received FCS
- Recomputes CRC over data
- Returns detailed validation result

---

## 🧪 Test Suite

The project includes comprehensive tests:

1. **Frame Generation** – Correct FCS calculation
2. **Valid Frame Verification** – Full round-trip test
3. **Error Detection** – Single-byte corruption test (demonstrates high sensitivity)

Even a **single-bit flip** causes the frame to be correctly rejected.

---

## 🛠️ How to Run

```bash
python crc_lab.py
```

**Expected Output**: All tests should pass with clear, formatted results.

---

## 📁 Project Structure

```bash
Ethernet-CRC32-Lab/
├── crc_lab.py              # Main script
├── README.md
```

---

## 🚀 Possible Extensions

- Add **lookup table** optimization (8x faster)
- Implement Ethernet **preamble + SFD**
- Add **frame padding** for frames smaller than 64 bytes
- Streaming CRC support for large data
- Bit-level visualization tool
- Comparison between software vs. hardware CRC

---

## ⚠️ Design Decisions

- **Bitwise implementation** chosen over lookup tables for educational clarity
- **Reflected polynomial** used to simulate real NIC behavior
- FCS stored in **little-endian** to match Ethernet wire format

---

## 👨‍💻 Technologies

- Python 3.8+
- No external dependencies

---

## 📜 License

This project is open source and available under the **MIT License**.

---

**Made for educational purposes** — perfect for Computer Networks, Operating Systems, and low-level systems programming courses.

---

**Feel free to star ⭐ the repository if you found it useful!**

```
