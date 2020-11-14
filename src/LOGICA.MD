# Project Name
Project Description

### Column Name
- [ ] Task title ~3d #type @name yyyy-mm-dd  
    - [ ] Sub-task or description  
    - [ ] Sub-task or description  
    - [ ] Sub-task or description  
        - [ ] Sub-task or description  

### Completed Column ✓
- [x] Completed task title  

==============
### Estrutura de dados

### Estados da Calculadora

Calculadora:

    VALUE: número atual no painel
    NUM1: Memória - Numero 1
    NUM2: Memória - Numero 2
    OP: Memória - Operador

    calcState:
        0:  
            - BOTÕES BLOQUEADOS: =
            - Aguardar digitação do primeiro, caso não VALUE = 0 |
                | Zero não é permitido antes do primeiro número
            - Caso Click em um operador + - * /:
                | copia VALUE para NUM1 e inserir operador em OP
                | Limpar VALUE
                | Mudar para estado 1
        1: 
            - Aparecer ZERO no painel (visor, apenas na UI), value = vazio
            - Usuário pode: digitar um valor, caso não VALUE = 0 | click no operador = + - * /
                | Caso click "="
                    | Inserir número em NUM2
                    | Calcular NUM1 OP NUM2, exemplo 10 * 5
                    | Inserir o resultado em VALUE
                    | Copiar VALUE para NUM1
                    | Zerar NUM2 e OP
                    | Mudar para estado 3
                | Caso click "+ - * /"
                    | Armazenar novo operador em variavel temporaria (TMP_OP)
                    | Inserir número em NUM2
                    | Calcular NUM1 OP NUM2, exemplo 10 * 5
                    | Inserir o resultado em VALUE
                    | Inserir o resultado em NUM1
                    | Copiar TMP_OP para OP
                    | Mudar para estado 3
        3:

    dotState:
        - true:
        - false:

### Estados de controle local

    DOTSTATE:
        Quando o usuário digita um ponto, o botão de ponto fica desabilitado. Só é permitido inserir um ponto.