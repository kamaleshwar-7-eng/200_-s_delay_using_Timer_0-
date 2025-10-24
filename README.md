# TIMER DELAY USING TIMER 0
# 8051 Program

## AIM
To write an assembly language program for the 8051 microcontroller to generate a 200 µs delay using Timer 0 in Mode 1 and toggle Port 0.1 repeatedly.
## APPARATUS REQUIRED
- Personal computer
- Keil μVision IDE

## ALGORITHM
1. Configure Timer 0 in Mode 1 (16-bit timer mode) using the TMOD register.
2. Load TH0 and TL0 registers with the initial value needed for a 200 µs delay (TH0 = 0xFF, TL0 = 0x38 for a 12 MHz clock).
3. Start Timer 0 by setting the TR0 bit.
4. Wait for the Timer 0 overflow flag (TF0) to be set.
5. Stop Timer 0 and clear the TF0 flag.
6. Toggle Port 0.1 using the CPL instruction.
7. Repeat the delay and toggle steps in an infinite loop.
```asm
ORG 0000H          
MOV TMOD, #01H     
AGAIN: MOV P1, #0FFH 
CALL DELAY         
MOV P1, #00H      
CALL DELAY         
SJMP AGAIN        
DELAY: MOV TH0, #0FFH 
       MOV TL0, #38  
       SETB TR0     
WAIT:  JNB TF0, WAIT
       CLR TR0       
       CLR TF0      
       RET         
END

```

## OUTPUT
<img width="1678" height="1000" alt="KAMALESH_SA2_7" src="https://github.com/user-attachments/assets/cda2609a-3d1b-4dbd-9f28-cf403f6a7891" />


## RESULT
The program toggles Port 0.1 continuously, with each transition occurring after a delay of approximately 200 µs, thus generating a square waveform at P0.1

