# EEG
The following python function helps you to reade edf.seizure file format that CHB-MIT dataset(https://physionet.org/content/chbmit/1.0.0/) use


```python
def read_edf_seizure_file(file):
    chars = list()
    seizuresStartTime = [0]
    seizureDuration = [0]
    char = "sss"
    with open(file, 'rb') as f:
        while len(char)>0:
            char = f.read(1)
            if len(char)> 0:
                chars.append(hex(ord(char)))
    numberOfSeizures = (chars.count("0xec")-1)//2   
    for i in range(1,numberOfSeizures+1):
        seizuresStartTime.append(seizureDuration[-1]+seizuresStartTime[-1]+append_hex(chars[22 + (i*16)],chars[25 + (i*16)]))
        seizureDuration.append(int(chars[33 + (i*16)],16))
    return numberOfSeizures,seizuresStartTime[1:],seizureDuration[1:]
```
