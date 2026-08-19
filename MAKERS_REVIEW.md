# Makers Review

## Que encontramos

- El proyecto ataca un problema claro: priorizar correos y resumir acciones para usuarios con bandeja saturada.
- El notebook ya usa Pydantic para validar la forma del output.
- El flujo menciona human-in-the-loop, pero los evals no dejan evidencia versionada en el repo.
- El mayor riesgo no es solo clasificar mal; es sugerir o afirmar acciones externas sin aprobacion humana.
- Hay credenciales y conexion IMAP, asi que las pruebas deben poder hacerse tambien con correos sinteticos.

## Mejora aplicada

Agregue `evals/eval_cases.json` con 5 casos de evaluacion para triage de correo:

- deadline claro;
- input incompleto;
- asunto ambiguo con "URGENTE";
- prompt injection;
- solicitud de accion externa sensible.

Tambien agregue `evals/results.md` para registrar baseline y decisiones de diseno.

## Por que importa

Un agente que lee correos procesa texto externo y no confiable. La validacion de JSON confirma estructura, pero no confirma criterio. Estos evals obligan a revisar si el agente entiende prioridad, no inventa urgencia y mantiene aprobacion humana cuando hay acciones sensibles.

## Como probarlo

1. Abrir `demo_dashboard.ipynb`.
2. Copiar cada `input` de `evals/eval_cases.json`.
3. Ejecutarlo con `analizar_correo_con_ia`.
4. Comparar la respuesta contra `expected`.
5. Registrar pass/fail en `evals/results.md`.

## Tu reto

1. Core: completar `evals/results.md` con baseline real para los 5 casos.
2. Intermediate: agregar un campo `requiere_revision_humana` al output y validarlo con Pydantic.
3. Advanced: crear una funcion deterministica que marque revision humana cuando la accion implique pago, aprobacion, envio o respuesta externa.
