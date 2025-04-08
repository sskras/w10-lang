# SPDX-License-Identifier: BlueOak-1.0.0
# SPDX-FileCopyrightText: 2024 Saulius Krasuckas <saulius2_at_ar-fi_point_lt> | sskras

A = An introductory description of this Makefile (a TODO).


all:
	@echo "${A}"
	@echo
	@echo "Available targets:"
	@
	@# Via: https://stackoverflow.com/questions/4219255/how-do-you-get-the-list-of-targets-in-a-makefile/26340367#26340367
	@$(MAKE) -pRrqn -f $(firstword $(MAKEFILE_LIST)) : 2> /dev/null \
	| awk                                                           \
	'                                           \
	      BEGIN                                 \
	      {                                     \
	          RS=""         # Set separators    \
	          FS=":"                            \
	      }                                     \
	                                            \
	      /^# Files$$/                          \
	      {                                     \
	          GO=1          # Start processing  \
	      }                                     \
	                                            \
	      /^# Finished Make data base/          \
	      {                                     \
	          GO=0          # Stop processing   \
	      }                                     \
	                                            \
	      GO && ! /^(#|\.|$@:)/                 \
	      {                                     \
	          printf "    " # Indent            \
	          print $$1     # Print target name \
	      }                                     \
	'                                           \
	| sort

desc:
	@echo "${A}"

get-lang:
	powershell 'Get-Culture; Get-WinSystemLocale; Get-WinUILanguageOverride; Get-WinUserLanguageList'
	C:/Windows/System32/Dism.exe //online //get-intl

extract:
	cd ISOs && time ../extract-winre-from-iso-images z.sha1 |& tee extract-winre-from-iso-images.log

out-files:
	@cd /ppool/BACKUPS/Ginto-Čebatoriūno--Thinkpad-Edge-E531/01-DEV-files       && \
	  rsync -avRH --info=progress2 --inplace /C/msys64* . --delete              && \
	  rsync -avRH --info=progress2 --inplace /C/ISOs* .                         && \
	  rsync -avRH --info=progress2 --inplace /C/Users/Renato/Downloads* .

out-rhash:
	@sh -c 'Dirs="/C/msys64 /C/ISOs /C/Users/Renato/Downloads"; (for Dir in $$Dirs; do cd $$Dir/..; Dirname=$$(basename $$Dir); rhash --sha1 -Pr $$Dirname | tee $$Dirname.sha1 ; done)'
