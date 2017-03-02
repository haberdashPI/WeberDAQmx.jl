# WeberDAQmx

This Julia package extends [Weber](https://github.com/haberdashPI/Weber.jl), to allow triggers to be sent during EEG recording using the DAQmx api. It is a simple extension which translates the record codes, during a call to `record`, to digital trigger events. It can be used as follows.

```julia
using Weber
using WeberDAQmx

# ... other setup code

exp = Experiment(
  # other settings...
  extensions = [daq_extension("/Device/port0/line0:7",
  	              codes=Dict("trial_start"=>0x01, "stimulus1" => 0x02))]
)

# expeirment setup continued...
```

Once extended, each record event (e.g. `moment(record,"stimulus1")`) will also send an event trigger (e.g. `0x02`).
