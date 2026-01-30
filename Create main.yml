Nome: Windows Cloud PC - Anydesk (Otimizado)

sobre:
  despacho de fluxo de trabalho:

empregos:
  construir:
    Nome: Iniciar Construção...
    executa em: windows-latest
    timeout-minutos: 10080 # Máximo de 7 dias para evitar tempo de execução excessivo

    passos:
      - nome: Baixando e Instalando o Essentials
        executar: |
          # Baixe o arquivo .bat para instalar componentes essenciais
          Invoke-WebRequest -Uri "https://www.dropbox.com/scl/fi/7eiczvgil84czu55dxep3/Downloads.bat?rlkey=wzdc1wxjsph2b7r0atplmdz3p&dl=1" -OutFile "Downloads.bat"
          # Executa o script .bat para instalar os componentes
          cmd /c Downloads.bat

      - nome: Entrar no AnyDesk
        executar: |
          # Verifique se o arquivo start.bat existe antes de executar
          se (Caminho-Teste "start.bat") {
            cmd /c iniciar.bat
          } outro {
            Write-Host "Arquivo start.bat não encontrado. Verifique a configuração."
          }

      - Nome: Monitorar e reiniciar o AnyDesk, se necessário
        executar: |
          # Monitore a conexão do AnyDesk e reinicie se necessário
          enquanto ($verdadeiro) {
            $process = Get-Process -Name "AnyDesk" -ErrorAction SilentlyContinue
            se (-não $process) {
              Write-Host "AnyDesk não está rodando, reiniciando..."
              cmd /c iniciar.bat
            }
            Start-Sleep -Seconds 300 # Verifique a cada 5 minutos
          }

      - nome: Contador de Tempo (Tarefa de Longa Duração)
        executar: |
          #Configura para manter a máquina em execução
          Start-Sleep -Seconds 604800 # 7 dias de execução contínua

      - nome: Limpar arquivos temporários
        if: sucesso() # Executa esta etapa apenas se todas as etapas anteriores foram bem-sucedidas
        executar: |
          # Remove arquivos temporários ou logs gerados
          Remove-Item Downloads.bat -Forçar
          Write-Host "Limpeza completa."
