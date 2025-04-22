from building import *
import os

# Import environment variables
Import('env')

# Get the current working directory
cwd = GetCurrentDir()

# Initialize include paths and source files list
path = [os.path.join(cwd, 'Include')]
src = [os.path.join(cwd, 'Source', 'Templates', 'system_stm32wlxx.c')]

# Map microcontroller units (MCUs) to their corresponding startup files
mcu_startup_files = {
    'STM32WL55xx': 'startup_stm32wle5xx.s',
    'STM32WLE5xx': 'startup_stm32wle5xx.s',
    'STM32WL54xx': 'startup_stm32wle4xx.s',
    'STM32WLE4xx': 'startup_stm32wle4xx.s',

}

# Check each defined MCU, match the platform and append the appropriate startup file
for mcu, startup_file in mcu_startup_files.items():
    if mcu in env.get('CPPDEFINES', []):
        if rtconfig.PLATFORM in ['gcc', 'llvm-arm']:
            src += [os.path.join(cwd, 'Source', 'Templates', 'gcc', startup_file)]
        elif rtconfig.PLATFORM in ['armcc', 'armclang']:
            src += [os.path.join(cwd, 'Source', 'Templates', 'arm', startup_file)]
        elif rtconfig.PLATFORM in ['iccarm']:
            src += [os.path.join(cwd, 'Source', 'Templates', 'iar', startup_file)]
        break

# Define the build group
group = DefineGroup('STM32WL-CMSIS', src, depend=['PKG_USING_STM32WL_CMSIS_DRIVER'], CPPPATH=path)

# Return the build group
Return('group')