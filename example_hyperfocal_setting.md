
If you want to set DxO One to specific mode, say aperture priority, manual focus, f/4 and focus to 3.7m


| Aperture | Hyperfocale | Sharpness range  |
|:--------:|:-----------:|:----------------:|
| f/1.8    | 7.8m        | 3.9m to infinity |
| f/2      | 7.4m        | 3.7m to infinity |
| f/2.8    | 5.2m        | 2.6m to infinity |
| f/4      | 3.7m        | 1.3m to infinity |
| f/5.6    | 2.6m        | 1.3m to infinity |
| f/8      | 1.8m        | 0.9m to infinity |
| f/11     | 1.3m        | 0.7m to infinity |

https://reference-dxoone.dxo.com/en/3-6-managing-focus/

type this on to autoexec.ash


# A mode
t svc json set_setting 52 7
# aperture to f/4
t svc json set_setting 30 7
# manual focus
t svc json set_setting 85 1
# move focus to 1/3.7m
t svc json set_setting 86 0.2702702702702703



