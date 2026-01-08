# 📚 ShaderToy Rim Effect

## Project Overview

이 프로젝트는 **Rim Lighting** 기법을 이용해 **역광 효과**를 구현한 shader이다.

Rim Lighting은 물체의 가장자리 부분을 밝게 강조하여 형태를 더 또렷하게 보이게 하며, 실시간 렌더링 환경에서 물체의 입체감과 현실성을 향상시키는데 사용된다.

본 구현에서는 **surface normal**과 **view direction**의 관계를 기반으로 Rim 효과를 계산하며, shader parameters를 통해 효과의 강도와 형태를 조절할 수 있도록 구성하였다.

---

## 📌 Key Concepts & Implementation

### **1) Normal과 View Direction의 Dot Product**
   
  Rim Lighting의 핵심은 물체 표면의 **Normal**과 **View Direction의 내적(dot product)** 이다.
  - 표면의 카메라를 향할수록 *N · V* 값은 1에 가까워지고
  - 실루엣(가장자리) 영역으로 갈수록 *N · V* 값은 0에 가까워진다.
    
  이를 이용해 다음과 같이 Rim Effect를 계산한다.
  -  **float rim = 1.0 - dot(input.normalWorld, toEye)**
    
  이 방식으로 **실루엣에 가까울수록 Rim Effect가 커지도록** 구현하였다.

---

### **2) Rim Power** 

  Rim Effect의 퍼짐 정도를 조절하기 위해 pow 함수를 적용한다.
  - **rim = pow(rim, rimPower)**
  - rimPower가 낮을수록 -> 넓고 부드러운 Rim
  - rimPower가 높을수록 -> 얇고 선명한 Rim
    
  이를 통해 세부적인 Rim Effect를 표현할 수 있다.

---

### **3) Smooth step**

  Rim 경계가 지나치게 날카롭게 보이는것을 방지하기 위해 **smoothstep**을 적용하였다.
  - **rim = smoothstep(0.0, 1.0, rim)**

  이를 통해 경계 영역에서 보다 자연스러운 그라데이션을 형성하여 사실성을 높인다.

---

### 🧩Code Snippet
<details>
  <summary><b></b></summary>

  <img width="720" alt="carbon (11)" src="https://github.com/user-attachments/assets/4e143a9c-dd01-473c-adf7-d8669e999fbf" />
</details>



## 📌 Sample Outputs

https://github.com/user-attachments/assets/c2a5551e-20b9-453d-a0a8-3410f2be16a6

---

## 📌 Future Work


---


## Development Environment

- Language: C++
- Graphics API: DirectX11
- Development Environment: Visual Studio 2022
- Build Configuration: x64, Debug / Release

### Hardware
- CPU: Intel CPU (Desktop)
- GPU: NVIDIA RTX 3060
- RAM: 16GB

### Platform
- OS: Windows 10 / 11
  
---

## References

- HongLab
  *Introduction to Computer Graphics with DirectX 11 – Part 2: Realtime Pipeline*
