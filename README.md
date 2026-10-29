# Avaliação de qualidade de sequências (Phred)

Página web estática para avaliar a qualidade de sequências de DNA com base em valores Phred. Roda inteiramente no navegador: nenhum arquivo é enviado a servidor.

## Formatos aceitos

| Formato | Observação |
|---|---|
| `.ab1` / `.abi` | Cromatograma ABIF; usa as bases e os valores de qualidade gravados pelo basecaller (tags `PBAS`/`PCON`) |
| `.phd.1` | Saída do Phred (bloco `BEGIN_DNA`) |
| `.fastq` / `.fq` | Qualidades Phred+33 |
| `.fasta` + `.qual` | Os nomes das sequências precisam coincidir nos dois arquivos |

## O que é calculado

- **CLR (região útil):** corte de qualidade pelo critério do `trim_alt` do Phred. Escolhe o trecho que maximiza a soma de `(pe − 10^(−Q/10))`, com `pe` = 0,05 por padrão.
- **Comprimento útil** e **Q médio** dentro do CLR.
- **Bases ≥ Q** (padrão Q20) e **bases ≥ Q30**, na sequência inteira.
- **Status:** *Aprovada* (comprimento útil e Q médio acima dos mínimos), *Limítrofe* (comprimento útil ≥ metade do mínimo) ou *Reprovada*. Todos os limiares são editáveis.
- Gráfico de qualidade por posição e sequência colorida por faixa de Q.
- Exportação: tabela CSV, FASTA e QUAL da região útil.

## Uso local

Abra `index.html` no navegador. Não há dependências nem etapa de build.

## Publicar no GitHub Pages

1. Crie um repositório e envie `index.html` e `README.md` para a branch `main`.
2. Em **Settings → Pages**, escolha **Deploy from a branch**, branch `main`, pasta `/ (root)`.
3. O site fica disponível em `https://<usuario>.github.io/<repositorio>/`.

## Limitações

- Os valores de qualidade de arquivos `.ab1` são os do basecaller do sequenciador, não uma nova chamada de bases pelo Phred. Para recalcular com o Phred original, rode o programa localmente e carregue os `.phd.1` gerados.
- Não há montagem (Phrap) nem remoção de vetor; o site avalia apenas qualidade.

## Licença

Adicione um arquivo `LICENSE` de sua escolha (por exemplo, MIT) pelo botão *Add file* do GitHub.
