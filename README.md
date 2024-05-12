
Fork of https://github.com/SeTSeR/esp-tm1637

It was too slow for my usecase, so i made it faster.   
Could have been fast before but i couldnt get it to go below a 30ms cycle....

It was remade with the ETS Delay from esp-idf-hal as delay provider, dunno if it works for non-std projects

Average Cycle is at 202us

# ESP IDF HAL Example
```rust
let pins = peripherals.pins;

let scl_pin = pins.gpio26;
let sda_pin = pins.gpio25;

let scl = PinDriver::input_output_od(scl_pin)?;
let sda = PinDriver::input_output_od(sda_pin)?;

let delay = Ets;

let mut tm1637 = TM1637::new(sda, scl, delay)?;


tm1637.send_number(1234, 0x7)?;

```
# Platform-agnostic driver for TM1637

This repository contains a driver for seven-segment display TM1637.
It was implemented using `embedded-hal`, so it should be platform-agnostic,
though examples use ESP32. Several examples are included, e. g. simple digital
[clocks](https://github.com/SeTSeR/esp32-tm1637/blob/master/examples/clocks.rs)
or just [sending some bytes around](https://github.com/SeTSeR/esp32-tm1637/blob/master/examples/send-digits.rs).

# Checking out

Building:
```sh
cargo build
```

Running an example:
```sh
cargo run --profile=lto --example=clocks
```
