# Aplicação De Postagens em arquitetura SOA

Esta é uma aplicação de criação e vizualização de posts, onde os usuários podem realizar um cadastro, ou logar em uma conta existente, e realizar e vizualizar suas postagens

## Como executar:

#### Windows:

Powershell (modo adm) caso não tenha nem docker nem k8s instalado
```bash
scripts\dev-setup.bat
scripts\install-dependencies.bat
```

Executar Docker
```bash
# inicialização completa(Realiza todos os scripts de uma vez)
scripts\start-complete.bat
```
```bash
# passo a passo
# Cria as imagens e containers no Docker
scripts\start-docker.bat

# Verifica se os serviços estão prontos e cria tópicos no kafka
scripts\wait-for-services.bat
scripts\create-kafka-topics.bat

# Realiza teste das rotas da API
scripts\test-api.bat

# Configura monitoramento com Prometheus e Grafana
scripts\monitoring-setup.bat

# Abre interfaces do Consul e Grafana no Navegador
scripts\monitor.bat
```

Executar k8s
```bash
scripts/deploy-k8s.bat
scripts/port-forward.bat
scripts/test-api.bat
```

Alguns scripts úteis
```bash
# Verifica o status completo dos serviços
scripts\check-services.bat
scripts\health-check.bat

# Verificar As métricas
scripts\check-metrics.bat
scripts\check-kafka.bat

# Para o projeto, apagando os containers
scripts\stop-docker.bat
scripts\delete-k8s.bat

# Limpar ambiente completamente
scripts\cleanup.bat

# Reinicia os serviços
scripts\restart-docker.bat
```


#### Unix
```bash
chmod +x scripts/*.sh
./scripts/start-docker.sh
```

#### k8s:
- Unix
```bash
chmod +x scripts/*.sh
./scripts/deploy-k8s.sh
```

## Testando API com cURL

```bash
# Teste completo automatizado
scripts\test-api-enhanced.bat

# Ou manualmente:

# Registrar usuário
curl -X POST http://localhost:8000/usuarios/registrar \
  -H "Content-Type: application/json" \
  -d '{"username":"john","password":"secret"}'

# Login
curl -X POST http://localhost:8000/usuarios/login \
  -H "Content-Type: application/json" \
  -d '{"username":"john","password":"secret"}'

# Criar post
curl -X POST http://localhost:8000/posts \
  -H "Content-Type: application/json" \
  -d '{"text":"Meu primeiro post","user_id":1}'

# Listar posts
curl http://localhost:8000/posts

# Verificar métricas
curl http://localhost:8000/metrics

# Health check
curl http://localhost:8000/health
```
