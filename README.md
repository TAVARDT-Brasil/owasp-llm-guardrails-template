# OWASP LLM01 Guardrails Template & Blueprint de Segurança de IA

[![Licence MIT](https://img.shields.io/badge/license-MIT-blue.svg)](LICENSE)
[![OWASP LLM01](https://img.shields.io/badge/OWASP-LLM01%20Hardened-ff0055.svg)](https://owasp.org/www-project-top-10-for-large-language-model-applications/)
[![Language](https://img.shields.io/badge/Language-Português-green.svg)](README.md)
[![AI Diagnostics](https://img.shields.io/badge/TAVARDT-AI%20Evaluator-5b3cf5.svg)](https://tools.tavardt.com/br/avaliador-robustez-llm/)
[![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)

Blueprint declarativo e middleware de código aberto para mitigação de Prompt Injection (OWASP LLM01), fuga de system prompt e ataques adversariais em agentes de IA, em conformidade com a LGPD e o Marco Legal da IA.

Desenvolvido e mantido pela equipe de engenharia da **TAVARDT**.

***

## 1. Visão Geral de Segurança para IA & LLMs

Este blueprint oferece uma biblioteca modular e leve (sem dependências pesadas) para implementar **guardrails determinísticos e heurísticos** em agentes autônomos, pipelines RAG e aplicações corporativas que consomem Large Language Models (OpenAI, Anthropic, Gemini, Llama, DeepSeek).

### Por que Guardrails são Críticos na Camada de Aplicação?
Modelos de linguagem não diferenciam instruções de sistema de dados fornecidos pelo usuário por padrão. Sem barreiras ativas na entrada (input guard) e na saída (output guard), aplicações de IA ficam vulneráveis ao sequestro de controle (jailbreak), exfiltração de chaves e dados confidenciais de clientes.

***

## 2. Vetores de Ameaça Cobertos (OWASP Top 10 for LLMs)

| Camada de Defesa | Vetor Mitigado | Descrição da Proteção |
| :- | :- | :- |
| **Input Sanitizer** | Injeção Direta de Prompt (Jailbreak) | Detecção de quebra de contexto (`ignore previous instructions`, `DAN`, deliminadores XML falsificados). |
| **Canary Token Verifier** | Fuga de System Prompt | Monitoramento de tokens canário invioláveis na saída para impedir exfiltração de regras confidenciais. |
| **RAG Boundary Guard** | Injeção Indireta via RAG | Isolamento semântico de documentos e fontes externas não confiáveis ingeridas na base vetorial. |
| **Structural Output Filter** | Manipulação de Ferramentas / MCP | Validação de chamadas de ferramentas e JSON schema para impedir execução de ações não autorizadas. |

***

## 3. Diagnóstico Prévio de Robustez do seu Modelo

Antes de colocar agentes cognitivos em contato com clientes ou sistemas internos, avalie o nível de suscetibilidade a jailbreaks e vazamentos através da ferramenta gratuita da TAVARDT:

* **Ferramenta de Avaliação:** Avaliador de Robustez de LLM TAVARDT
* **Catálogo Global de Diagnósticos:** **TAVARDT Tools Brasil**

***

## 4. Instalação & Guia de Uso Rápido

### Clonar & Executar

```bash
git clone https://github.com/TAVARDT-Brasil/owasp-llm-guardrails-template.git
cd owasp-llm-guardrails-template
python examples/quickstart.py
```

### Exemplo de Integração em Python

```python
from guardrails.validator import LLMGuardrail

guard = LLMGuardrail()

# 1. Validação de Ingress (Input Guardrail)
is_safe, error = guard.validate_input(user_input)
if not is_safe:
    raise ValueError(f"Entrada bloqueada por padrão suspeito: {error}")

# 2. Injeção de Canary no Prompt de Sistema
hardened_system_prompt = guard.get_canary_injection_prompt(system_prompt)

# 3. Validação de Egress (Output Guardrail)
is_valid, leak_error = guard.validate_output(completion)
if not is_valid:
    raise SecurityError("Falha crítica: Vazamento de system prompt detectado!")
```

***

## 5. Consultoria Especializada em Segurança de IA & Agentes Autônomos

Caso sua organização desenvolva agentes autônomos de atendimento (WhatsApp/Telegram/Web), sistemas RAG sensíveis ou necessite de auditoria perimetral de IA corporativa:

* **Portal Corporativo:** **TAVARDT**
* **Atendimento Técnico Especializado:** [Entrar em Contato com a Engenharia](https://ag.tavardt.com/br/contato/)

***

## Licença

Distribuído sob a licença de código aberto MIT. Consulte o arquivo [`LICENSE`](LICENSE) para mais detalhes.  
Copyright

***

## Governança e Soberania

* **Unidade Soberana**: **TAVARDT Brasil** (`TAVARDT-Brasil`)
* **Normas Centrais**: [00-core Governança](https://github.com/TAVARDT-Brasil/00-core)
* **Central de Diagnósticos**: **Central de Ferramentas TAVARDT**
* **Segurança Corporativa**: [TAVARDT Cibersegurança](https://ag.tavardt.com/br/ciberseguranca/)

***

### Licença
Distribuído sob a Licença MIT. Consulte o arquivo [LICENSE](LICENSE) para obter detalhes completos.

***

© 2026 TAVARDT. Todos os direitos reservados.
