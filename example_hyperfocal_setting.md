
If you want to set DxO One to specific mode, say aperture priority, manual focus, f/4 and focus to 3.7m



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


