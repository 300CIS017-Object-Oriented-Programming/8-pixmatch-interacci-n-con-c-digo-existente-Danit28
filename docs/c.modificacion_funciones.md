
## Evidencia del cambio
> Ponga aquí evidencia con imágenes y fragmento de código

#### Archivo Json guarda 4 jugadores

#### Interfa gráfica muestra cuatro jugadores

def Leaderboard(what_to_do):
    # Esta parte se encarga de crear la tabla de clasificacion, de los puntajes
    if what_to_do == 'create':
        # Crea la tabla de clasificación si no existe y el nombre del jugador está proporcionado
        if mystate.GameDetails[3] != '' and not os.path.isfile(vpth + 'leaderboard.json'):
            tmpdict = {}
            json.dump(tmpdict, open(vpth + 'leaderboard.json', 'w'))  # Escribir archivo

    elif what_to_do == 'write':
        # Guarda el puntaje del jugador en la tabla de clasificación si el nombre está proporcionado
        if mystate.GameDetails[3] != '':
            if os.path.isfile(vpth + 'leaderboard.json'):
                leaderboard = json.load(open(vpth + 'leaderboard.json'))  # Leer archivo
                leaderboard_dict_lngth = len(leaderboard)

                leaderboard[str(leaderboard_dict_lngth + 1)] = {'NameCountry': mystate.GameDetails[3],
                                                                'HighestScore': mystate.myscore}
                leaderboard = dict(sorted(leaderboard.items(), key=lambda item: item[1]['HighestScore'],
                                          reverse=True))  # Ordenar de forma descendente

                if len(leaderboard) > 4:  # Mostrar los cuatro principales jugadores
                    for i in range(len(leaderboard) - 4):
                        leaderboard.popitem()  # Eliminar último jugador

                json.dump(leaderboard, open(vpth + 'leaderboard.json', 'w'))  # Escribir archivo

    elif what_to_do == 'read':
        # Leer puntajes y mostrar a los cuatro principales jugadores en la interfaz gráfica
        if mystate.GameDetails[3] != '':
            if os.path.isfile(vpth + 'leaderboard.json'):
                leaderboard = json.load(open(vpth + 'leaderboard.json'))  # Leer archivo

                leaderboard = dict(sorted(leaderboard.items(), key=lambda item: item[1]['HighestScore'],
                                          reverse=True))  # Ordenar de forma descendente

                sc0, sc1, sc2, sc3, sc4 = st.columns((2, 2, 2, 2, 2))
                rknt = 0
                for vkey in leaderboard.keys():
                    if leaderboard[vkey]['NameCountry'] != '':
                        rknt += 1
                        if rknt == 1:
                            sc0.write('🏆 Top Players:')
                            sc1.write(
                                f"🥇 | {leaderboard[vkey]['NameCountry']}: *{leaderboard[vkey]['HighestScore']}*")
                        elif rknt == 2:
                            sc2.write(
                                f"🥈 | {leaderboard[vkey]['NameCountry']}: *{leaderboard[vkey]['HighestScore']}*")
                        elif rknt == 3:
                            sc3.write(
                                f"🥉 | {leaderboard[vkey]['NameCountry']}: *{leaderboard[vkey]['HighestScore']}*")
                        elif rknt == 4:
                            sc4.write(
                                f"4️⃣ | {leaderboard[vkey]['NameCountry']}: *{leaderboard[vkey]['HighestScore']}*")

#### Usuario pierde el juego cuando supera un máximo posible de fallos.

## Encuesta de la experiencia
Por favor, responde las siguientes preguntas basadas en tu experiencia modificando el código para incluir cuatro personas en el leaderboard en lugar de tres.

**Nombre:**

#### 1. ¿Cuánto tiempo te llevó entender las secciones del código relacionada con el leaderboard?
- [ ] Menos de 10 minutos
- [ ] Entre 10 y 30 minutos
- [ ] Entre 30 minutos y 1 hora
- [*] Más de 1 hora

#### 2. ¿Cuánto tiempo te llevó entender las secciones del código relacionada con hacer que el usuario pierda si supera x cantidad de turnos?
- [ ] Menos de 10 minutos
- [ ] Entre 10 y 30 minutos
- [ ] Entre 30 minutos y 1 hora
- [*] Más de 1 hora

#### 3. ¿Consideras que estaba documentada la lógica en el código para facilitar el cambio?
- [ ] Sí
- [*] No

#### 4. ¿Te pareció fácil identificar dónde y qué cambios realizar para aumentar el número de personas en el leaderboard de 3 a 4?
- [ ] Muy fácil
- [ ] Algo fácil
- [*] Algo difícil
- [ ] Muy difícil


#### 5. ¿Te pareció fácil identificar dónde y qué cambios realizar para agregar la lógica de perder el juego?
- [ ] Muy fácil
- [ ] Algo fácil
- [ ] Algo difícil
- [*] Muy difícil


#### 5. ¿Qué tan seguro te sientes de que tus cambios no introdujeron errores en otras áreas del código?
- [ ] Muy seguro
- [ ] Moderadamente seguro
- [*] Poco seguro
- [ ] Nada seguro

#### 6. Después de realizar los cambios, ¿cuánto tiempo te tomó verificar que el cambio funcionó como se esperaba?
- [ ] Menos de 10 minutos
- [ ] Entre 10 y 30 minutos
- [*] Entre 30 minutos y 1 hora
- [ ] Más de 1 hora

#### 7. ¿Qué estrategia usaste para verificar que no habían problemas en el código fuente?

#### 8. ¿Te enfrentaste a algún problema mientras intentabas realizar los cambios? Si es así, ¿cómo lo resolviste?
- [ ] No enfrenté problemas
- [ ] Revisé la documentación del código
- [*] Busqué ayuda de un compañero o en línea
- [ ] Otro (especificar)
