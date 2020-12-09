<template>
  <div class="survey">
    <survey :survey="survey"></survey>
    <link href="https://unpkg.com/survey-vue@1.8.18/modern.css" type="text/css" rel="stylesheet" />
  </div>
</template>

<script src="https://unpkg.com/survey-vue@1.8.18/survey.vue.min.js"></script>

<script>
import * as SurveyVue from "survey-vue";
import "survey-vue/survey.css";

SurveyVue.StylesManager.applyTheme("darkblue");

var Survey = SurveyVue.Survey;

export default {
  name: "survey-restaurante-x",
  components: {
    Survey,
  },
  data() {
    var json = {
      locale: "pt",
      pages: [
        {
          name: "page1",
          elements: [
            {
              type: "html",
              name: "question2",
              minWidth: "500px",
              html: {
                default:
                  "Buscamos sempre melhorar e para isso precisamos da sua ajuda! Gostaríamos de saber um pouco mais sobre a sua experiência conosco, e para isso, é só clicar no botão abaixo e responder algumas perguntas:",
                pt:
                  "Buscamos sempre melhorar e para isso precisamos da sua ajuda! Gostaríamos de saber um pouco mais sobre a sua experiência conosco, e para isso, é só informar o seu nome, clicar no botão abaixo e responder algumas perguntas:"
              }
            },
            {
              type: "text",
              name: "nome",
              title: {
                pt: "Nome:"
              },
              hideNumber: true
            }
          ],
          questionTitleLocation: "top",
          title: "Bem Vindo(a), cliente do Restaurante X!",
          questionsOrder: "initial"
        },
        {
          name: "page2",
          elements: [
            {
              type: "radiogroup",
              name: "ambiente",
              width: "600px",
              minWidth: "600px",
              maxWidth: "600px",
              title:
                "Como você classifica o ambiente? (Salão, bar, banheiros...)",
              commentText: "Como podemos melhorar?",
              choices: [
                {
                  value: "1",
                  text: "Ótimo"
                },
                {
                  value: "2",
                  text: "Bom"
                },
                {
                  value: "3",
                  text: "Regular"
                },
                {
                  value: "4",
                  text: "Ruim"
                }
              ],
              otherText: "Ruim",
              colCount: 5
            },
            {
              type: "comment",
              name: "comentario1",
              visibleIf: "{ambiente} anyof [3, 4]",
              width: "600px",
              minWidth: "600px",
              maxWidth: "600px",
              title: {
                pt: "Como podemos melhorar?"
              },
              hideNumber: true
            }
          ],
          maxTimeToFinish: 2
        },
        {
          name: "page3",
          elements: [
            {
              type: "radiogroup",
              name: "cardapio",
              width: "600px",
              minWidth: "600px",
              maxWidth: "600px",
              title: "Como você classifica o cardápio?",
              commentText: "Sugestão de novos pratos ou melhorias?",
              choices: [
                {
                  value: "1",
                  text: "Ótimo"
                },
                {
                  value: "2",
                  text: "Bom"
                },
                {
                  value: "3",
                  text: "Regular"
                },
                {
                  value: "4",
                  text: "Ruim"
                }
              ],
              otherText: "Ruim",
              colCount: 5
            },
            {
              type: "comment",
              name: "comentario2",
              visibleIf: "{cardapio} anyof [3, 4]",
              width: "600px",
              minWidth: "600px",
              maxWidth: "600px",
              title: {
                pt: "Como podemos melhorar?"
              },
              hideNumber: true
            }
          ],
          visibleIf: "{cardapio} anyof ['Ruim']"
        },
        {
          name: "page4",
          elements: [
            {
              type: "radiogroup",
              name: "atendimento",
              width: "600px",
              minWidth: "600px",
              maxWidth: "600px",
              title: "Como classifica o nosso atendimento?",
              commentText: "Como podemos melhorar?",
              choices: [
                {
                  value: "1",
                  text: "Ótimo"
                },
                {
                  value: "2",
                  text: "Bom"
                },
                {
                  value: "3",
                  text: "Regular"
                },
                {
                  value: "4",
                  text: "Ruim"
                }
              ],
              otherText: "Ruim",
              colCount: 5
            },
            {
              type: "comment",
              name: "comentario3",
              visibleIf: "{atendimento} anyof [3,4]",
              width: "600px",
              minWidth: "600px",
              maxWidth: "600px",
              title: {
                pt: "Como podemos melhorar?"
              },
              hideNumber: true
            }
          ]
        },
        {
          name: "page5",
          elements: [
            {
              type: "rating",
              name: "experiencia",
              width: "600px",
              minWidth: "600px",
              maxWidth: "600px",
              title:
                "De forma geral, como classifica a sua experiência no Restaurante X?"
            },
            {
              type: "radiogroup",
              name: "recomendacao",
              visibleIf: "{experiencia} > 2",
              width: "600px",
              minWidth: "600px",
              maxWidth: "600px",
              title: {
                pt: "Recomendaria o Restaurante X a um amigo(a)?"
              },
              hideNumber: true,
              choices: [
                {
                  value: "1",
                  text: {
                    pt: "Sim"
                  }
                },
                {
                  value: "2",
                  text: {
                    pt: "Não"
                  }
                }
              ]
            }
          ]
        }
      ],
      showProgressBar: "bottom",
      goNextPageAutomatic: true,
      firstPageIsStarted: true
    };

    var model = new SurveyVue.Model(json);

    model.onComplete.add(function(result) {
      document.querySelector("#surveyResult").textContent = JSON.stringify(
        result.data,
        null,
        3
      );
    });

    return {
      survey: model
    };
  
  }
};
</script>