## **Nome, arroba e bio**

* **Nome, arroba e bio são compatíveis com outros perfis conhecidos.**  
  * Confirme o handle em instagram.com/USERNAME (sem @) e registre: nome exibido, arroba, foto, bio, link e contadores básicos (posts, seguidores, seguindo).  
  * Use buscadores de username (coleções tipo Osintgram, InstagramOSINT Tool e outros “Instagram OSINT tools”) para puxar metadados estruturados: ID numérico, tipo de conta (pessoal/empresa), status de verificação, se é pública ou privada.  
  * Faça buscas com dorks em motores de busca: "@username" site:instagram.com, "username" "instagram" e combinações com nome completo ou apelido para achar menções externas, leaks e perfis relacionados.

---

## **Foto de perfil, estética e linguagem**

* **Foto de perfil, estética e linguagem são coerentes com a hipótese investigativa.**  
  * Baixe a foto de perfil com ferramentas como Osintgram (propic) ou serviços de visualização/“InstaDP” recomendados em tutoriais de Instagram OSINT, mantendo cópia em alta resolução para análise.  
  * Faça busca reversa da foto (Google Images, Yandex, Bing Visual, OSINT.LINK) para ver se a mesma imagem aparece em outras redes, sites pessoais, notícias ou documentos — isso ajuda a ligar identidades com nomes diferentes.  
  * Compare estilo de linguagem (gírias, emojis, tom de legenda) e estética geral (cores, filtros, enquadramento) com perfis já mapeados da mesma pessoa em TikTok, YouTube, X, etc., como sugerem guias de correlação multi‑plataforma.

---

## **Feed, cenário e rotina**

* **O feed apresenta padrões de cenário, pessoas, temas ou rotina.**  
  * Role o feed observando: locais recorrentes, tipos de ambiente (casa, escola, trabalho, academia), pessoas que aparecem repetidamente e objetos marcantes (uniformes, logotipos, veículos, símbolos de grupos).  
  * Em cada post relevante, verifique timestamp (mouse sobre a data na web) e, se houver, localização marcada; analisar horários e locais ao longo do tempo permite inferir padrões de rotina (trabalho, estudo, lazer).  
  * Quando precise de maior volume de dados, use ferramentas como Instaloader/Instalooter ou Osintgram para baixar posts públicos com legendas, hashtags e datas, mantendo um dataset estruturado para análise séria (sem simular scraping de contas privadas).

---

## **Destaques e stories em destaque**

* **Destaques preservam conteúdos úteis sobre escola, eventos, viagens, grupos ou vínculos.**  
  * Examine cada coleção de **Highlights** (destaques) e anote quais temas aparecem: viagens, festas, esportes, fandoms, eventos de escola/faculdade, etc.; guias SOCMINT destacam que destaques funcionam como “currículo visual condensado”.  
  * Em stories fixados com locais, banners de evento ou crachás, use novamente geotags, nomes próprios e logotipos para pivotar para buscas externas (Google, LinkedIn, sites de escolas e clubes).  
  * Quando relevante para o caso e permitido pela política interna, capture e arquive destaques com ferramentas de download de stories (Instaloader, Osintgram stories), registrando data/hora da coleta e a URL do perfil para manter cadeia de custódia.

---

## **Reels, repertório cultural e crosspost com TikTok**

* **Reels indicam repertório cultural, trends e possível crosspost com TikTok.**  
  * Use a aba de **Reels** para observar trilhas sonoras, trends, challenges e formatos de humor/estética — isso ajuda a situar o perfil em comunidades (fandoms, nichos políticos, subculturas estéticas).  
  * Para investigar crosspost, copie o link do Reel, baixe ou extraia o thumbnail e faça busca reversa para ver se o mesmo vídeo (ou corte) aparece em TikTok, YouTube Shorts ou outras plataformas.  
  * Ferramentas de coleta como Osintgram (mediatype, photos, captions) ou InstagramOSINT podem gerar listagens com tipo de mídia, datas, legendas e hashtags, facilitando ver quais Reels são reupload de outros lugares.

---

## **Comentários, marcações e menções**

* **Comentários, marcações e menções revelam conexões sociais observáveis.**  
  * Abra a aba de **marcados** (TAGGED) para ver posts de terceiros em que o alvo foi marcado; isso costuma revelar círculo social próximo e conexões familiares ou profissionais.  
  * Nos posts próprios, leia comentários e veja quem mais interage com frequência (mesmos perfis curtindo/comentando sempre) — guias de Instagram OSINT sugerem mapear “inner circle” por densidade de interação, não apenas por lista de seguidores.  
  * Ferramentas como Osintgram (tagged, wcommented, wtagged) e OSINTGraph (que importa seguidores/seguidos para Neo4j) permitem transformar essa rede em grafo, evidenciando conexões fortes, contas “ponte” e eventuais alts ligados por padrão de conexões.

---

## **Conta principal, secundária ou reserva**

* **Há sinais de conta principal, secundária ou reserva.**  
  * Observe se a conta tem **nome real**, foto clara, grande número de conexões familiares/colegas e histórico longo de posts; materiais de investigação indicam que esse conjunto tende a sinalizar conta principal.  
  * Perfis com poucos seguidores, baixa exposição (sem foto clara), conteúdo mais solto/experimental ou temáticas muito específicas (ex.: “finsta”, memes internos, fandom extremo) podem ser perfis secundários ou de reserva — trate isso como hipótese, não fato.  
  * Ferramentas de análise de rede como OSINTGraph (comparando sobreposição de seguidores/seguidos, clusters de comunidade) e suítes como IG‑Detective ajudam a detectar padrões de conexões atípicos que sugerem alts ou sock puppets.

---

## **Confirmação em outras fontes/plataformas**

* **Achados foram confirmados em outra fonte ou plataforma antes de qualquer conclusão forte.**  
  * Guias especializados insistem que evidência de Instagram deve ser cruzada com outras fontes: outras redes sociais, registros públicos, notícias, documentos e, se for o caso, dados internos da organização.  
  * Use reverse image search, dorks em motores de busca e plataformas de social media lookup (focadas em correlação de perfis) para verificar se detalhes de bio, fotos e padrões de linguagem aparecem de forma consistente fora do Instagram.  
  * Para preservar evidência de maneira defensável, recomenda‑se capturar páginas com ferramentas forenses/web‑archiving (Pagefreezer, Webrecorder, Wayback) e manter registro de data/hora, URL, ferramenta e escopo de coleta, como descrito nos guias de coleta “defensável”.
