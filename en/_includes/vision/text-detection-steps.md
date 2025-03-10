1. Prepare an image file that meets the requirements:

    [!INCLUDE [file-restrictions](../../_includes/vision/file-restrictions.md)]

    > [!NOTE]
    >
    > Need a sample image? Download an image of the [penguin crossing](https://storage.yandexcloud.net/vision/penguins_sample.jpg) road sign.

1. Encode the file as Base64:

    [!INCLUDE [base64-encode-command](base64-encode-command.md)]

1. Create a file with the request body (for example, `body.json`). In the `content` property, specify the [Base64-encoded](../../vision/operations/base64-encode.md) image.
In the recognition settings, list the languages that image text might be written in, such as English (`en`). You can specify from 1 to 8 languages:

    **body.json:**

    ```json
    {
        "folderId": "ajk55f3mblj12eghq2oe",
        "analyze_specs": [{
            "content": "iVBORw0KGgo...",
            "features": [{
                "type": "TEXT_DETECTION",
                "text_detection_config": {
                    "language_codes": ["en"]
                }
            }]
        }]
    }
    ```

1. [!INCLUDE [send-request](send-request.md)]

    The response will consist of recognized blocks of text, lines, and words with their position on the image indicated:

    ```json
    {
      "results": [{
        "results": [{
          "textDetection": {
            "pages": [{
              "blocks": [{
                "boundingBox": { ... },
                "lines": [{
                    "boundingBox": { ... },
                    "words": [{
                      "boundingBox": {
                        "vertices": [{
                            "x": "504",
                            "y": "760"
                          },
                          {
                            "x": "504",
                            "y": "836"
                          },
                          {
                            "x": "826",
                            "y": "836"
                          },
                          {
                            "x": "826",
                            "y": "760"
                          }
                        ]
                      },
                      "languages": [{
                        "languageCode": "en",
                        "confidence": 0.9520227313
                      }],
                      "text": "PENGUINS",
                      "confidence": 0.9520227313
                    }],
                    "confidence": 0.9520227313
                  },
                  ...
                ]
              }],
              "width": "1920",
              "height": "1280"
            }]
          }
        }]
      }]
    }
    ```

1. To get all the recognized words from the image, find all the lines with the `text` property (one way to do this is using the [grep](https://www.gnu.org/software/grep/) utility):

    ```bash
    $ grep -o "\"text\":\s\".*\"" output.json
    "text": "PENGUINS"
    "text": "CROSSING"
    "text": "SLOW"
    ```

