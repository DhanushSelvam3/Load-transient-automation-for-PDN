This Python-based automation script tests the stability of a Power Distribution Network (PDN) in Dynamic transient test in each rails

Overview
1) The script configures your Electronic Load to pulse current and your Oscilloscope to capture the peak overshoot &b undershoot
2) It triggers a load jump from 10% to 90% load in a specified slew rate and captures the voltage waveform.
3) It queries the Scope for the exact Peak (Vmax) and Dip (Vmin) to check if they stay within your defined 5% tolerance.
4) It saves the raw signal data as a CSV file for deep analysis.
5) It generates a final spreadsheet summarizing the Pass/Fail status of all power rails.

The requirements
1) An Electronic Load and an Oscilloscope capable of SCPI/VISA communication.
2) Libraries: `pyvisa`, `pandas`
3) Drivers: Ensure NI-VISA or Keysight IO Libraries are installed so the computer can communicate to the instruments.

Set-ups
1.  Configure Rails: Update the `RAILS` dictionary at the top of the script with your board's specific voltages and currents.
2.  Update Addresses: In the if _name_ == _main_: block, replace the placeholder VISA strings with the actual addresses of your devices (find these using your instrument software like Keysight Connection Expert).
    
Outputs
1)Console Summary
2)Waveform Data
3)Master Report

Note:
The script uses a `finally` block to ensure `TRAN OFF` is always sent, preventing the electronic load from overheating your board if the script encounters an error.
Tolerance: The script assumes a ±5% tolerance. If your design requires tighter (e.g., 2%) or looser (e.g., 10%) limits, change the `tolerance` value in the `RAILS` dictionary.
