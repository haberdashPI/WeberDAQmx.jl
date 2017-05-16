# WeberDAQmx

This Julia package extends [Weber](https://github.com/haberdashPI/Weber.jl), to
allow triggers to be sent during EEG recording using the
[DAQmx api](https://www.ni.com/dataacquisition/nidaqmx.htm). It is a simple
extension which translates the record codes, during a call to `record`, to
digital trigger events.


# Example

The following experiment sends the code 0x01 to port0 on TestDevice.

```julia
port = "/TestDevice/port0/line0:7"
experiment = Experiment(extensions=[
  @DAQmx(port;eeg_sample_rate=512,codes=Dict("test" => 0x01))])
setup(experiment) do
  addtrial(moment(record,"test"))
end
run(experiment)
```
