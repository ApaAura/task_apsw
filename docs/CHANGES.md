# Modificări și teste

## Bug-uri corectate

| Nr. | Reproducere | Problema | Soluție |
|---|---|---|---|
| 1 | Dashboard, card "In progress" | Arăta mereu 0, compara cu `In Progress` | Comparație cu `In progress` |
| 2 | Dashboard, link "View all" | Ducea la `/task` (redirect la Overview) | Link către `/tasks` |
| 3 | Projects, "View project" | Link `/project/:id` duce la Overview | Link către `/projects/:id` |
| 4 | Șterge un task | După ștergere navigare la `/task` | Navigare la `/tasks` |
| 5 | Tasks, filtru status "In progress" | Nu returna nimic (`In Progress`) | Comparație directă cu statusul |
| 6 | Tasks, căutare după asignee cu litere mici | Căutarea era case-sensitive și crăpa fără asignee | Căutare case-insensitive, tolerantă la lipsă |
| 7 | Formular, titlu doar spații | Se salva un titlu gol | `trim()` la validare și la trimitere |
| 8 | Editează un task și schimbă proiectul | `projectId` salvat ca string, proiectul dispărea | Conversie la `Number` |
| 9 | Sidebar, badge Tasks | Număr fix `7` | Număr real din API, reîmprospătat la navigare |
| 10 | Dashboard cu API oprit | Eroare ignorată, fără mesaj | Mesaj de eroare afișat |

Extra: `projectId` implicit din formular era `1` hardcodat (acum primul proiect încărcat), linkul de proiect din detalii nu mai duce la `/projects/` când lipsește proiectul, iar `api.js` nu mai lasă `options` să suprascrie header-ele.

## Funcționalitate nouă

Filtru după prioritate (Low, Medium, High, All priorities) în pagina Tasks, combinat cu căutarea și statusul. Controlul are `aria-label`, contorul "Showing X of Y" reflectă filtrarea, starea goală are buton de resetare, iar butonul "Reset filters" apare când e activ un filtru.

## Teste

- `npm run build` fără erori.
- API: POST, PATCH, DELETE și `GET /tasks?priority=High` verificate cu curl.
- Manual: filtre combinate, listă goală, formular cu titlu gol, navigare între pagini, ștergere cu redirect.
