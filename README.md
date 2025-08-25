# Generic_SISO_shift_register
This project implements a **parameterized Serial-In Serial-Out (SISO) shift register** in Verilog, along with a self-checking testbench.

## 🔹 The Model (`shift_reg_siso.v`)

- **Parameters**
  - `WIDTH` → size of the shift register (default: 4, can be 8, 16, …).
  - `RESET_VALUE` → value after reset (default: all zeros).

- **Inputs**
  - `clk` → clock (shifting happens on rising edge).
  - `reset_n` → asynchronous active-low reset.
  - `en` → enable (only shift when high).
  - `dir` → shift direction (`0 = left`, `1 = right`).
  - `sdi` → serial data input bit.

- **Output**
  - `sdo` → serial data output bit:
    - MSB (`[WIDTH-1]`) when shifting left.
    - LSB (`[0]`) when shifting right.

➡️ In simple words: every clock tick, the register shifts in the selected direction and brings in the new bit from `sdi`. After `WIDTH` clocks, that bit emerges at `sdo`.


## 🔹 The Testbench (`tb_shift_reg_siso.v`)

- Generates a **1 MHz clock** (`timescale 1us/1ns`).
- Applies **reset**, then feeds sequences of bits.
- Uses a **golden reference model** inside the testbench to replicate the DUT’s behavior.
- On every clock, the DUT is compared to the golden reference:
  - If they match → test continues.
  - If they mismatch → an **ERROR** is printed.
- `$monitor` prints signal states so you can watch bits moving through the register.

➡️ This testbench is self-checking — it acts like a **scoreboard**, verifying DUT automatically.


## 🔹 How to Run

### Run on [EDA Playground](https://www.edaplayground.com/)
1. Create a new Verilog playground.
2. Paste both `shift_reg_siso.v` and `tb_shift_reg_siso.v`.
3. Select **Icarus Verilog** or **Verilator** for easy waveform viewing.
4. Run simulation:
   - Check console for `$monitor` output.
   - Open EPWave to view waveforms.


