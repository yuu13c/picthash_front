<template>
  <v-row justify="center">
    <v-col cols="8">
      <v-row>
        <v-col cols=12 sm="12" md="12" lg="4">
          <v-card class="pa-3" flat tile>
            <v-card-text>
              <p class="headline text--primary text-left">
                シンプルな操作
              </p>
              <p class="text-left text--primary">
                難しい操作は一切ありません。あなたの画像を選んで、ボタンをクリックするだけで始めることができます。
              </p>
            </v-card-text>
          </v-card>
        </v-col>
        <v-col cols=12 sm="12" md="12" lg="4">
          <v-card class="pa-3" flat tile>
            <v-card-text>
              <p class="headline text--primary text-left">
                代表的な画像ファイルに対応
              </p>
              <p class="text-left text--primary">
                JPEGやBMP、PNGなどの代表的な画像ファイルに対応しています。
              </p>
            </v-card-text>
          </v-card>
        </v-col>
        <v-col cols=12 sm="12" md="12" lg="4">
          <v-card class="pa-3" flat tile>
            <v-card-text>
              <p class="headline text--primary text-left">
                高精度なハッシュ値算出
              </p>
              <p class="text-left text--primary">
                同じ画像は同じハッシュ値に。似たような画像は似たようなハッシュ値に。
              </p>
            </v-card-text>
          </v-card>
        </v-col>
      </v-row>
    </v-col>
  </v-row>
</template>

<script>
export default {
  name: 'Description',
  data: () => ({
      //
  })
}
</script>