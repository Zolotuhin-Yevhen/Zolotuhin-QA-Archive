@echo off
setlocal

:: 1. Название архива (можешь поменять на любое)
set "ZIP_NAME=QA_Pack_New.zip"

echo [START] Собираю все файлы в этой папке...

:: 2. Команда PowerShell:
:: -Exclude исключает сам батник и уже созданный архив, чтобы не было ошибки "файл занят"
powershell -Command "Get-ChildItem -Path . -Exclude '%~nx0', '%ZIP_NAME%' | Compress-Archive -DestinationPath '.\%ZIP_NAME%' -Force"

if %errorlevel% equ 0 (
    echo.
    echo [SUCCESS] Архив %ZIP_NAME% готов!
) else (
    echo.
    echo [ERROR] Ошибка при создании архива.
)

pause