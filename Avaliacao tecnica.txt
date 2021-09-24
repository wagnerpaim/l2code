-- L2Code

--A quantidade de horas que cada professor tem comprometido em aulas - Então faça uma consulta SQL que traga essa informação.

SELECT SUM(H.numhoras), PROF.codprof, PROF.nomeprof
FROM PROFESSOR PROF
INNER JOIN PROFTURMA PT ON PT.coddepto = PROF.coddepto AND PT.codprof = PROF.codprof
INNER JOIN TURMA T ON T.coddepto = PT.coddepto AND T.numdisc = PT.numdisc AND T.siglatur = PT.siglatur 
INNER JOIN HORARIO H ON H.coddepto = T.coddepto AND H.numdisc = T.numdisc AND H.siglatur = T.siglatur
GROUP BY SUM(H.numhoras), PROF.codprof, PROF.nomeprof;

--Lista de salas com horários livres e ocupados, e qual o professor que está ministrando a aula

SELECT S.numsala, S.descricaosala, S.codpredio, P.descricaopredio, H.diasem, H.horainicio, T.anosem, T.siglatur, D.numdisc, D.nomedisc, P.codprof, TIT.nometit
FROM SALA S
INNER JOIN PREDIO P ON P.codpredio = S.codpredio
INNER JOIN HORARIO H ON H.codpredio = S.codpredio AND H.numsala = S.numsala
INNER JOIN TURMA T ON T.coddepto = H.coddepto AND T.numdisc = H.numdisc AND T.anosem = H.anosem AND T.siglatur = H.siglatur
INNER JOIN DISCIPLINA D ON D.coddepto = T.coddepto AND D.numdisc = T.numdisc
INNER JOIN PROFTURMA PT ON PT.coddepto = T.coddepto AND PT.numdisc = T.numdisc AND PT.anosem = T.anosem AND PT.siglatur = T.siglatur
INNER JOIN PROFESSOR PROF ON PROF.codprof = PT.codprof AND PROF.coddepto = PT.coddepto
INNER JOIN TITULACAO TIT ON TIT.codtit = PROF.codtit
ORDER BY H.diasem, H.horainicio;