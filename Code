ASSEMBLY LANGUAGE PROGRAM:
   ; Setting the reset vector to start the program at MAIN
   ORG 00H                  ; Set the reset vector to address 00H
   LJMP MAIN                ; Jump to the MAIN subroutine
  ; Defining the lookup table for 7-segment display data
   ORG 300H                 ; Set the memory location for the lookup table
   TBL:   DB 0C0H,0F9H,0A4H,0B0H,99H,92H,82H,0F8H,80H,90H    ; 7-seg data for common anode type
   ; Starting address for the main program
    ORG 30H                    ; Set the starting address of the main program   
    MAIN:                        ; Main subroutine starts here
     ; Initializing port P2 and P3
     MOV P2,#00H          ; Initialize port P2
     MOV P3,#00H          ; Initialize port P3
     ; Call subroutine to set the front direction
     ACALL FRONT       ; Call subroutine FRONT
    ; Initialize DPTR to point to the lookup table
    MOV DPTR,#TBL        ; Load DPTR with the address of the lookup table
    ; Initialize loop counters
    CLR A                       ; Clear accumulator A
    MOV 40H,#10          ; Initialize 40H
    MOV 43H,#10          ; Initialize 43H
    MOV 46H,#10          ; Initialize 46H
    MOV 49H,#20          ; Initialize 49H
    MOV R0,#35           ; Initialize loop counter R0
    MOV R6,#30           ; Initialize loop counter R6
    MOV R7,#40           ; Initialize loop counter R7

X1:                                 ; Loop X1 starts here
    ; Calculate and display the first digit of the number for 40H
    MOV A,40H            ; Move the value of 40H to accumulator A
    MOV B,#10            ; Move the value 10 to register B
    DIV AB                   ; Divide accumulator A by register B
    MOV 41H,A            ; Store quotient in 41H
    MOV 42H,B            ; Store remainder in 42H
A1:                               ; Subroutine A1 starts here
    ; Display the first digit of the number for 40H
    SETB P3.0              ; Set bit P3.0 (common anode for 7-segment display)
    CLR P3.1                ; Clear bit P3.1 (common anode for 7-segment display)
    MOV A,41H           ; Move the value of 41H to accumulator A
    MOVC A,@A+DPTR       ; Move data from lookup table to accumulator A
    MOV P2,A               ; Move accumulator A to port P2
    ACALL DELAY      ; Call delay subroutine
    MOV P3,#00H         ; Clear port P3
    SETB P3.1               ; Set bit P3.1 (common anode for 7-segment display)
    CLR P3.0                 ; Clear bit P3.0 (common anode for 7-segment display)
    MOV A,42H           ; Move the value of 42H to accumulator A
    MOVC A,@A+DPTR       ; Move data from lookup table to accumulator A
    MOV P2,A               ; Move accumulator A to port P2
    ACALL DELAY      ; Call delay subroutine
    MOV P3,#00H         ; Clear port P3
    SJMP X3                  ; Jump to loop X3
X2:                               ; Loop X2 starts here
    SJMP X1                 ; Jump to loop X1
X3:                              ; Loop X3 starts here
    ; Continue with similar operations for other registers
    ; Decrement loop counter and repeat if not zero
    DJNZ R0,X2            ; Decrement R0 and jump to X2 if not zero
    MOV R0,#35            ; Reload R0 with initial value
    ; Jump to Q1
    DJNZ 40H,Q1           ; Decrement 40H and jump to Q1 if not zero
    MOV 40H,#20           ; Reload 40H with initial value
    ; Q1, Q2, Q3, Q4, X4, and L1 are similar loops...
    DELAY:                   ; Subroutine DELAY starts here
    ; Delay subroutine
    MOV R4,#5                        ; Load R4 with 5
    H2: MOV R5,#0FFH         ; Load R5 with 0FFH (255)
    H1: DJNZ R5,H1               ; Decrement R5 and jump to H1 if not zero
     DJNZ R4,H2                    ; Decrement R4 and jump to H2 if not zero
    RET                                   ; Return from subroutine 
; Subroutines to set the direction of LEDs
FRONT:                               ; Subroutine FRONT starts here
    MOV P1,#54H                ; Move value to P1 to control LED direction
    MOV P0,#02H                ; Move value to P0 to control LED direction
    RET                                 ; Return from subroutine

RIGHT:                             ; Subroutine RIGHT starts here
    MOV P1,#0A1H         ; Move value to P1 to control LED direction
    MOV P0,#02H            ; Move value to P0 to control LED direction
    RET                             ; Return from subroutine

BACK:                           ; Subroutine BACK starts here
    MOV P1,#09H          ; Move value to P1 to control LED direction
    MOV P0,#05H          ; Move value to P0 to control LED direction
    RET                           ; Return from subroutine
LEFT:                            ; Subroutine LEFT starts here
    MOV P1,#4AH          ; Move value to P1 to control LED direction
    MOV P0,#08H          ; Move value to P0 to control LED direction
    RET    
